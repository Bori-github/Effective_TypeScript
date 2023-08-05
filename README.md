# Effective TypeScript | Bori Lee

《이펙티브 타입스크립트: 동작 원리의 이해와 구체적인 조언 62가지》 책을 기반으로 공부한 내용을 기록합니다.

[Effective TypeScript 스터디 레포지토리 바로가기](https://github.com/Gamangjum-lihou/effective-typescript-study)

- **Chapter 1: Getting to Know TypeScript**

  - [ ] [:memo: Item 1][Item 1]: Understand the Relationship Between TypeScript and JavaScript
  - [ ] [:memo: Item 2][Item 2]: Know Which TypeScript Options You’re Using
  - [x] [:memo: Item 3][Item 3]: Understand That Code Generation Is Independent of Types
  - [ ] [:memo: Item 4][Item 4]: Get Comfortable with Structural Typing
  - [ ] [:memo: Item 5][Item 5]: Limit Use of the any Type

- **Chapter 2: TypeScript’s Type System**

  - [ ] [:memo: Item 6][Item 6]: Use Your Editor to Interrogate and Explore the Type System
  - [ ] [:memo: Item 7][Item 7]: Think of Types as Sets of Values
  - [x] [:memo: Item 8][Item 8]: Know How to Tell Whether a Symbol Is in the Type Space or Value Space
  - [ ] [:memo: Item 9][Item 9]: Prefer Type Declarations to Type Assertions
  - [ ] [:memo: Item 10][Item 10]: Avoid Object Wrapper Types (String, Number, Boolean, Symbol, BigInt)
  - [ ] [:memo: Item 11][Item 11]: Recognize the Limits of Excess Property Checking
  - [x] [:memo: Item 12][Item 12]: Apply Types to Entire Function Expressions When Possible
  - [x] [:memo: Item 13][Item 13]: Know the Differences Between type and interface
  - [ ] [:memo: Item 14][Item 14]: Use Type Operations and Generics to Avoid Repeating Yourself
  - [ ] [:memo: Item 15][Item 15]: Use Index Signatures for Dynamic Data
  - [x] [:memo: Item 16][Item 16]: Prefer Arrays, Tuples, and ArrayLike to number Index Signatures
  - [ ] [:memo: Item 17][Item 17]: Use readonly to Avoid Errors Associated with Mutation
  - [ ] [:memo: Item 18][Item 18]: Use Mapped Types to Keep Values in Sync

- **Chapter 3: Type Inference**

  - [ ] [:memo: Item 19][Item 19]: Avoid Cluttering Your Code with Inferable Types
  - [x] [:memo: Item 20][Item 20]: Use Different Variables for Different Types
  - [ ] [:memo: Item 21][Item 21]: Understand Type Widening
  - [ ] [:memo: Item 22][Item 22]: Understand Type Narrowing
  - [ ] [:memo: Item 23][Item 23]: Create Objects All at Once
  - [x] [:memo: Item 24][Item 24]: Be Consistent in Your Use of Aliases
  - [ ] [:memo: Item 25][Item 25]: Use async Functions Instead of Callbacks for Asynchronous Code
  - [ ] [:memo: Item 26][Item 26]: Understand How Context Is Used in Type Inference
  - [ ] [:memo: Item 27][Item 27]: Use Functional Constructs and Libraries to Help Types Flow

- **Chapter 4: Type Design**

  - [x] [:memo: Item 28][Item 28]: Prefer Types That Always Represent Valid States
  - [ ] [:memo: Item 29][Item 29]: Be Liberal in What You Accept and Strict in What You Produce
  - [ ] [:memo: Item 30][Item 30]: Don’t Repeat Type Information in Documentation
  - [x] [:memo: Item 31][Item 31]: Push Null Values to the Perimeter of Your Types
  - [ ] [:memo: Item 32][Item 32]: Prefer Unions of Interfaces to Interfaces of Unions
  - [ ] [:memo: Item 33][Item 33]: Prefer More Precise Alternatives to String Types
  - [ ] [:memo: Item 34][Item 34]: Prefer Incomplete Types to Inaccurate Types
  - [x] [:memo: Item 35][Item 35]: Generate Types from APIs and Specs, Not Data
  - [ ] [:memo: Item 36][Item 36]: Name Types Using the Language of Your Problem Domain
  - [ ] [:memo: Item 37][Item 37]: Consider “Brands” for Nominal Typing

- **Chapter 5: Working with any**

  - [ ] [:memo: Item 38][Item 38]: Use the Narrowest Possible Scope for any Types
  - [x] [:memo: Item 39][Item 39]: Prefer More Precise Variants of any to Plain any
  - [ ] [:memo: Item 40][Item 40]: Hide Unsafe Type Assertions in Well-Typed Functions
  - [ ] [:memo: Item 41][Item 41]: Understand Evolving any
  - [ ] [:memo: Item 42][Item 42]: Use unknown Instead of any for Values with an Unknown Type
  - [x] [:memo: Item 43][Item 43]: Prefer Type-Safe Approaches to Monkey Patching
  - [ ] [:memo: Item 44][Item 44]: Track Your Type Coverage to Prevent Regressions in Type Safety

- **Chapter 6: Types Declarations and @types**

  - [ ] :memo: Item 45: Put TypeScript and @types in devDependencies
  - [ ] :memo: Item 46: Understand the Three Versions Involved in Type Declarations
  - [x] [:memo: Item 47][Item 47]: Export All Types That Appear in Public APIs
  - [ ] [:memo: Item 48][Item 48]: Use TSDoc for API Comments
  - [ ] [:memo: Item 49][Item 49]: Provide a Type for this in Callbacks
  - [ ] [:memo: Item 50][Item 50]: Prefer Conditional Types to Overloaded Declarations
  - [x] [:memo: Item 51][Item 51]: Mirror Types to Sever Dependencies
  - [ ] [:memo: Item 52][Item 52]: Be Aware of the Pitfalls of Testing Types

- **Chapter 7: Writing and Running Your Code**

  - [ ] [:memo: Item 53][Item 53]: Prefer ECMAScript Features to TypeScript Features
  - [ ] [:memo: Item 54][Item 54]: Know How to Iterate Over Objects
  - [x] [:memo: Item 55][Item 55]: Understand the DOM hierarchy
  - [ ] [:memo: Item 56][Item 56]: Don’t Rely on Private to Hide Information
  - [ ] [:memo: Item 57][Item 57]: Use Source Maps to Debug TypeScript

- **Chapter 8. Migrating to TypeScript**
  - [ ] [:memo: Item 58][Item 58]: Write Modern JavaScript
  - [ ] [:memo: Item 59][Item 59]: Use @ts- [ ]check and JSDoc to Experiment with TypeScript
  - [ ] :memo: Item 60: Use allowJs to Mix TypeScript and JavaScript
  - [ ] [:memo: Item 61][Item 61]: Convert Module by Module Up Your Dependency Graph
  - [ ] [:memo: Item 62][Item 62]: Don’t Consider Migration Complete Until You Enable noImplicitAny

[Item 1]: /ch01-intro/item-01-ts-vs-js
[Item 2]: /ch01-intro/item-02-which-ts
[Item 3]: /ch01-intro/item-03-independent
[Item 4]: /ch01-intro/item-04-structural
[Item 5]: /ch01-intro/item-05-any
[Item 6]: /ch02-types/item-06-editor
[Item 7]: /ch02-types/item-07-types-as-sets
[Item 8]: /ch02-types/item-08-type-value-space
[Item 9]: /ch02-types/item-09-prefer-declarations-to-assertions
[Item 10]: /ch02-types/item-10-avoid-object-wrapper-types
[Item 11]: /ch02-types/item-11-excess-property-checking
[Item 12]: /ch02-types/item-12-type-entire-functions
[Item 13]: /ch02-types/item-13-type-vs-interface
[Item 14]: /ch02-types/item-14-map-between-types
[Item 15]: /ch02-types/item-15-index-for-dynamic
[Item 16]: /ch02-types/item-16-number-index
[Item 17]: /ch02-types/item-17-readonly
[Item 18]: /ch02-types/item-18-values-in-sync
[Item 19]: /ch03-inference/item-19-avoid-inferable
[Item 20]: /ch03-inference/item-20-one-var-one-type
[Item 21]: /ch03-inference/item-21-widening
[Item 22]: /ch03-inference/item-22-narrowing
[Item 23]: /ch03-inference/item-23-all-at-once
[Item 24]: /ch03-inference/item-24-avoid-aliasing
[Item 25]: /ch03-inference/item-25-use-async-await
[Item 26]: /ch03-inference/item-26-context-inference
[Item 27]: /ch03-inference/item-27-well-typed-libs
[Item 28]: /ch04-design/item-28-valid-states
[Item 29]: /ch04-design/item-29-loose-accept-strict-produce
[Item 30]: /ch04-design/item-30-jsdoc-repeat
[Item 31]: /ch04-design/item-31-null-values-to-perimeter
[Item 32]: /ch04-design/item-32-union-of-interfaces
[Item 33]: /ch04-design/item-33-avoid-strings
[Item 34]: /ch04-design/item-34-incomplete-over-innacurate
[Item 35]: /ch04-design/item-35-consider-codegen
[Item 36]: /ch04-design/item-36-language-of-domain
[Item 37]: /ch04-design/item-37-brands
[Item 38]: /ch05-any/item-38-narrowest-any
[Item 39]: /ch05-any/item-39-specific-any
[Item 40]: /ch05-any/item-40-hide-unsafe-casts
[Item 41]: /ch05-any/item-41-evolving-any
[Item 42]: /ch05-any/item-42-never-unknown
[Item 43]: /ch05-any/item-43-type-safe-monkey
[Item 44]: /ch05-any/item-44-type-percentage
[Item 47]: /ch06-declarations/item-47-export-your-types
[Item 48]: /ch06-declarations/item-48-use-tsdoc
[Item 49]: /ch06-declarations/item-49-this-in-callbacks
[Item 50]: /ch06-declarations/item-50-conditional-overload
[Item 51]: /ch06-declarations/item-51-mirror-types-for-deps
[Item 52]: /ch06-declarations/item-52-test-your-types
[Item 53]: /ch07-write-run/item-53-avoid-non-ecma
[Item 54]: /ch07-write-run/item-54-iterate-objects
[Item 55]: /ch07-write-run/item-55-understand-the-dom
[Item 56]: /ch07-write-run/item-56-private-rely
[Item 57]: /ch07-write-run/item-57-source-maps-debug
[Item 58]: /ch08-migrate/item-58-write-modern-js
[Item 59]: /ch08-migrate/item-59-jsdoc-tscheck
[Item 61]: /ch08-migrate/item-61-convert-up-the-graph
[Item 62]: /ch08-migrate/item-62-start-loose
