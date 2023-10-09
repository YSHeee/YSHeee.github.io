# Tailwind CSS

## Installation

### tailwind CLI

Install nvm [->](https://ysheee.github.io/note/pm2/)

- nvm (Node Version Manager) : Node.js의 버전 관리
- npm (Node Package Manager)
  <br>: JavaScript 패키지(라이브러리, 프레임워크 등)를 관리하고 설치하는 도구
  <br>: Node.js와 함께 제공되며 패키지의 설치, 업데이트, 삭제 등을 쉽게 처리할 수 있도록 도와준다

Step to Step ([Docs-Tailwind CLI](https://tailwindcss.com/docs/installation))

### play CDN

Add the Play CDN script to your HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="https://cdn.tailwindcss.com"></script>
  </head>
  <body>
    <h1 class="text-3xl font-bold underline">Hello world!</h1>
  </body>
</html>
```

Step to Step ([Docs-Play CDN](https://tailwindcss.com/docs/installation/play-cdn))

---

## Core Concepts

### Utility-First Fundamentals

=== "with tailwindCSS"
    ``` html
    <!-- 기존 클래스를 HTML에 적용하여 스타일 지정 -->
    <div class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-lg flex items-center space-x-4">
      <div class="shrink-0">
        <img class="h-12 w-12" src="/img/logo.svg" alt="ChitChat Logo">
      </div>
      <div>
        <div class="text-xl font-medium text-black">ChitChat</div>
        <p class="text-slate-500">You have a new message!</p>
      </div>
    </div>
    ```
=== "기존 CSS"
    ``` html
    <!-- 스타일을 지정할 때마다 CSS 작성 -->
    <div class="chat-notification">
      <div class="chat-notification-logo-wrapper">
        <img class="chat-notification-logo" src="/img/logo.svg" alt="ChitChat Logo">
      </div>
      <div class="chat-notification-content">
        <h4 class="chat-notification-title">ChitChat</h4>
        <p class="chat-notification-message">You have a new message!</p>
      </div>
    </div>
    <style>
      .chat-notification {
        display: flex;
        max-width: 24rem;
        margin: 0 auto;
        padding: 1.5rem;
        border-radius: 0.5rem;
        background-color: #fff;
        box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
      }
      .chat-notification-logo-wrapper {
        flex-shrink: 0;
      }
      .chat-notification-logo {
        height: 3rem;
        width: 3rem;
      }
      .chat-notification-content {
        margin-left: 1.5rem;
        padding-top: 0.25rem;
      }
      .chat-notification-title {
        color: #1a202c;
        font-size: 1.25rem;
        line-height: 1.25;
      }
      .chat-notification-message {
        color: #718096;
        font-size: 1rem;
        line-height: 1.5;
      }
    </style>
    ```

- flexbox, padding : `flex`, `shrink-0`, `p-6`
- max-width, margin : `max-w-sm`, `mx-auto`
- background-color, border radius, box-shadow : `bg-white`, `rounded-xl`, `shadow-lg`
- width, height : `w-12`, `h-12`
- space-between : `space-x-4`
- font-size, text color, font-weight : `text-xl`, `text-black`, `font-medium`

**Tailwind CSS의 이점?**

- You aren’t wasting energy inventing class names
- Your CSS stops growing
- Making changes feels safer

---
### [Hover, Focus, and Other States](https://tailwindcss.com/docs/hover-focus-and-other-states)

#### Tailwind CSS modifiers

- Pseudo-classes : `:hover`, `:focus`, `:first-child`, `:visited`, ... `:{required}`
- Pseudo-elements : `::before`, `::after`, `::placeholder`, ... `::{selection}`
- Media and feature queries : `prefers-reduced-motion`, 다크 모드, 반응형 breakpoint 등
- Attribute selectors : `[dir="rtl"]`, `[open]`, ...

=== "Hover, focus, and active"
    ``` html title="Example"
    <button class="bg-violet-500 hover:bg-violet-600 active:bg-violet-700 focus:outline-none focus:ring focus:ring-violet-300 ...">
      Save changes
    </button>
    ```
=== "First, last, odd, and even"
    ``` html
    <ul role="list" class="p-6 divide-y divide-slate-200">
      {#each people as person}
        <!-- Remove top/bottom padding when first/last child -->
        <li class="flex py-4 first:pt-0 last:pb-0">
          <img class="h-10 w-10 rounded-full" src="{person.imageUrl}" alt="" />
          <div class="ml-3 overflow-hidden">
            <p class="text-sm font-medium text-slate-900">{person.name}</p>
            <p class="text-sm text-slate-500 truncate">{person.email}</p>
          </div>
        </li>
      {/each}
    </ul>
    ```
=== "Form states"
    ``` html
    <form>
      <label class="block">
        <span class="block text-sm font-medium text-slate-700">Username</span>
        <!-- Using form state modifiers, the classes can be identical for every input -->
        <input type="text" value="tbone" disabled class="mt-1 block w-full px-3 py-2 bg-white border border-slate-300 rounded-md text-sm shadow-sm placeholder-slate-400
          focus:outline-none focus:border-sky-500 focus:ring-1 focus:ring-sky-500
          disabled:bg-slate-50 disabled:text-slate-500 disabled:border-slate-200 disabled:shadow-none
          invalid:border-pink-500 invalid:text-pink-600
          focus:invalid:border-pink-500 focus:invalid:ring-pink-500
        "/>
      </label>
      <!-- ... -->
    </form>
    ```

<br>

#### Styling based on parent state

- group-{modifier} : 상위 요소의 상태에 따라 요소의 스타일을 지정해야 하는 경우 
- group/{name} : 중첩된 그룹 구별
- group-* : 임시 부모 그룹 생성 (Arbitrary groups)
- peer-{modifier} : 형제 요소의 상태에 따라 요소의 스타일 지정
- peer-checked/{name} : 형제 요소 구별
- peer-* : 임시 형제 그룹 생성 (Arbitrary peers)

=== "group-{modifier}"
    ``` html title="Example"
    <a href="#" class="group block max-w-xs mx-auto rounded-lg p-6 bg-white ring-1 ring-slate-900/5 shadow-lg space-y-3 hover:bg-sky-500 hover:ring-sky-500">
      <div class="flex items-center space-x-3">
        <svg class="h-6 w-6 stroke-sky-500 group-hover:stroke-white" fill="none" viewBox="0 0 24 24"><!-- ... --></svg>
        <h3 class="text-slate-900 group-hover:text-white text-sm font-semibold">New project</h3>
      </div>
      <p class="text-slate-500 group-hover:text-white text-sm">Create a new project from a variety of starting templates.</p>
    </a>
    ```
=== "Arbitrary groups"
    ``` html
    <div class="group is-published">
      <div class="hidden group-[.is-published]:block">
        Published
      </div>
    </div>
    ```

<br>

#### Pseudo-classes, Pseudo-Element
- Before and after
- Placeholder text
- File input buttons
- List markers
- Highlighted text
- First-line and first-letter
- Dialog backdrops

=== "after"
    ``` html
    <label class="block">
      <span class="after:content-['*'] after:ml-0.5 after:text-red-500 block text-sm font-medium text-slate-700">
        Email
      </span>
      <input type="email" name="email" class="mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md sm:text-sm focus:ring-1" placeholder="you@example.com" />
    </label>
    ```
=== "placeholder"
    ``` html
    <label class="relative block">
      <span class="sr-only">Search</span>
      <span class="absolute inset-y-0 left-0 flex items-center pl-2">
        <svg class="h-5 w-5 fill-slate-300" viewBox="0 0 20 20"><!-- ... --></svg>
      </span>
      <input class="placeholder:italic placeholder:text-slate-400 block bg-white w-full border border-slate-300 rounded-md py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm" placeholder="Search for anything..." type="text" name="search"/>
    </label>
    ```
=== "file"
    ``` html
    <!-- <input type="file" class="file:border file:border-solid ..." /> -->
    <input type="file" class="block w-full text-sm text-slate-500
      file:mr-4 file:py-2 file:px-4
      file:rounded-full file:border-0
      file:text-sm file:font-semibold
      file:bg-violet-50 file:text-violet-700
      hover:file:bg-violet-100
    "/>
    ```
=== "file&Highlighted"
    ``` html
    <ul role="list" class="marker:text-sky-400 list-disc pl-5 space-y-3 text-slate-400">
    <div class="selection:bg-fuchsia-300 selection:text-fuchsia-900"> <!-- 텍스트 선택 시 하이라이트 -->
    ```
=== "First"
    ``` html
    <p class="first-line:uppercase first-line:tracking-widest
      first-letter:text-7xl first-letter:font-bold first-letter:text-white
      first-letter:mr-3 first-letter:float-left
    ">
    ```
=== "Dialog backdrops"
    ``` html
    <dialog class="backdrop:bg-gray-50">
      <form method="dialog">
        <!-- ... -->
      </form>
    </dialog>
    ```

<br>

#### Media and feature queries
- Responsive breakpoints
- Prefers color scheme : light, dark theme
- Prefers reduced motion
- Prefers contrast
- Viewport orientation
- Print styles
- Supports rules

=== "Responsive"
    ``` html
    <!-- 반응형 modifier `md`, `lg` -->
    <div class="grid grid-cols-3 md:grid-cols-4 lg:grid-cols-6">
      <!-- ... -->
    </div>
    ```
=== "Prefers reduced motion"
    ``` html
    <!-- 모션 -->
    <button type="button" class="bg-indigo-500 ..." disabled>
      <svg class="motion-reduce:hidden animate-spin ..." viewBox="0 0 24 24"><!-- ... --></svg>
      Processing...
    </button>
    ```

<br>

#### Attribute selectors
- ARIA states
- RTL support :star:
- Open/closed state

#### Custom modifiers

---
### [Responsive Design](https://tailwindcss.com/docs/responsive-design)
: 반응형 웹 디자인 구축

| Breakpoint prefix  | Minimum width |
| :----------------: | :-----------: |
| sm | 	640px | 
| md | 	768px |
| lg | 1024px |
| xl | 1280px |
| 2xl | 1536px |

``` html
<!-- Width of 16 by default, 32 on medium screens, and 48 on large screens -->
<img class="w-16 md:w-32 lg:w-48" src="...">
```

---
### [스타일 재사용](https://tailwindcss.com/docs/reusing-styles) Loops

=== "each"
    ``` html
    <div class="mt-3 flex -space-x-2 overflow-hidden">
      {#each contributors as user}
        <img class="inline-block h-12 w-12 rounded-full ring-2 ring-white" src="{user.avatarUrl}" alt="{user.handle}"/>
      {/each}
    </div>
    ```
=== "map"
    ``` html
    <nav className="flex sm:justify-center space-x-4">
      {[
        ['Home', '/dashboard'],
        ['Team', '/team'],
        ['Projects', '/projects'],
        ['Reports', '/reports'],
      ].map(([title, url]) => (
        <a href={url} className="rounded-lg px-3 py-2 text-slate-700 font-medium hover:bg-slate-100 hover:text-slate-900">{title}</a>
      ))}
    </nav>
    ```

---
### [사용자 정의 스타일 추가](https://tailwindcss.com/docs/adding-custom-styles)

---
!!! quote
    - [Docs](https://tailwindcss.com/docs/installation)
    - openai



