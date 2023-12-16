# RecipeVariants
> [Type error: use Omit or Pick with RecipeVariants<X> #527](https://github.com/vanilla-extract-css/vanilla-extract/issues/527)  

`Recipes` 패키지의 `RecipeVariants`를 사용하면 컴포넌트 스타일에 대한 타입을 쉽게 생성할 수 있다.  
Vanilla Extract가 어떤 이유로 이러는지 모르겠지만 `RecipeVariants`는 `undefined`를 포함한 타입을 리턴한다. 

### Property 'size' does not exist on type 'ButtonVariants'
```ts
import { recipe, RecipeVariants } from "@vanilla-extract/recipes";

// Get the type
export type ButtonVariants = RecipeVariants<typeof button>;

// Button.tsx 
type size = ButtonVariants['size']; // Property 'size' does not exist on type 'ButtonVariants'
```
당연히 'ButtonVariants'에 존재할 것이라고 생각한 `size`는 존재하지 않는다는 메세지를 확인할 수 있다. 

```ts
(alias) type ButtonVariants = {
    ...
} | undefined
```
다시 `ButtonVariants`를 살펴보면, 해당 타입은 `undefined`를 포함한다는 것을 알 수 있다.     

#### vanilla-extract-recipes.cjs.d.ts
```ts
// ...
type RuntimeFn<Variants extends VariantGroups> = ((options?: VariantSelection<Variants>) => string) & {
    variants: () => (keyof Variants)[];
    classNames: RecipeClassNames<Variants>;
};

type RecipeVariants<RecipeFn extends RuntimeFn<VariantGroups>> = Resolve<Parameters<RecipeFn>[0]>;
```

`recipes` 패키지의 타입 정의 파일 `.d.ts`를 살펴보면 대충 원인은 알 수 있다.  
`RuntimeFn` 타입의 `options?: ...`에서 옵셔널 파라미터를 지워보니 해당 오류는 발생하지 않는 걸 봐서 저기가 문제인 것 같다...!  

무슨 연유든 `RecipeVariants`는 `undefined`를 포함한 타입을 리턴한다는 점을 확인했다.

### 해결 방법 : NonNullable\<T\> 

```ts
export type ButtonVariants = NonNullable<RecipeVariants<typeof button>>;
```
유틸리티 타입 `NonNullable<T>`를 사용하여 T에서 `null` 과 `undefined`를 제외한 타입을 구성한다. 
