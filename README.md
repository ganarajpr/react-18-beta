# Next.js _12.0.4_ and React 18 _Beta_ Demo & Benchmark

Next.js 12 comes with [React 18 Beta support](https://nextjs.org/blog/next-12#preparing-for-react-18).

React 18 will add features like Suspense, automatic batching of updates, APIs
like `startTransition`, and a new streaming API for server rendering with
support for `React.lazy`.

_This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app)._

_This project referenced the [Next.js 12.0.1 **React 18 Alpha**
Demo](https://github.com/cedrickchee/next-rsc-demo/) (released on Oct 27)._

[**React 18 usage in Next.js**](https://nextjs.org/docs/advanced-features/react-18)

I'm making these features available to try today in Next.js 12. This project
have the beta version of React installed:

```sh
$ npm install next@latest react@beta react-dom@beta
```

I have enabled these advanced features (Alpha quality):

- **Server-Side Streaming**: Concurrent features in React 18 include built-in
  support for server-side Suspense and SSR streaming support. This allows you to
  server-render pages using HTTP streaming. This is an experimental feature in
  Next.js 12, but once enabled, SSR will use the same strict runtime as
  Middleware. Enabled using the experimental flag `concurrentFeatures: true` in
  `next.config.js`. (See
  [docs](https://nextjs.org/docs/advanced-features/react-18#enable-ssr-streaming-alpha)
  for more details)

- **React Server Components**: React Server Components allow us to render
  everything, including the components themselves, on the server. This is
  fundamentally different from server-side rendering where you're pre-generating
  HTML on the server. With Server Components, there's zero client-side
  JavaScript needed, making page rendering faster. This improves the user
  experience of your application, pairing the best parts of server-rendering
  with client-side interactivity. Enabled using the experimental flag
  `serverComponents: true`. (See
  [docs](https://nextjs.org/docs/advanced-features/react-18#react-server-components)
  for more details)

This is the demo of Hacker News built with Next.js and React Server Components.

**Try the demo: https://next-news-rsc.vercel.sh**

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Compile

```sh
$ npm run build

> build
> next build

warn  - You have enabled experimental feature(s).
warn  - Experimental features are not covered by semver, and may cause unexpected or broken application behavior. Use them at your own risk.

info  - Checking validity of types  

info  - Need to disable some ESLint rules? Learn more here: https://nextjs.org/docs/basic-features/eslint#disabling-rules
info  - Using the createRoot API for React
warn  - You are using an unsupported prerelease of 'react-dom' which may cause unexpected or broken application behavior. Continue at your own risk.
warn  - You are using the experimental Edge Runtime with `concurrentFeatures`.
warn  - You have experimental React Server Components enabled. Continue at your own risk.
info  - Creating an optimized production build  
info  - Compiled successfully
info  - Collecting page data  
Page                                       Size     First Load JS
┌ ℇ /                                      1.97 kB        78.9 kB
├   /_app                                  0 B            76.9 kB
├ λ /404                                   384 B          77.3 kB
├ λ /500                                   393 B          77.3 kB
├ λ /api/hello                             0 B            76.9 kB
├ ℇ /csr                                   3.36 kB        80.3 kB
├ ℇ /rsc                                   2.31 kB        79.2 kB
├ ℇ /slow                                  3.32 kB        80.2 kB
└ ℇ /ssr                                   2.57 kB        79.5 kB
+ First Load JS shared by all              76.9 kB
  ├ chunks/framework-f4a6e75f8d3c80e4.js   44.9 kB
  ├ chunks/main-5d1d5b9b49f6a7f4.js        30 kB
  ├ chunks/pages/_app-7961434b35938642.js  587 B
  └ chunks/webpack-f5637e6c804d3e68.js     1.42 kB

ℇ  (Streaming)  server-side renders with streaming (uses React 18 SSR streaming or Server Components)
λ  (Server)     server-side renders at runtime (uses getInitialProps or getServerSideProps)
```

## Performance and UX Benchmark

I have been casually tracking and researching the progress of [the plan for React 18](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html). I have tested multiple React 18 versions since, from Alpha release to the current [Beta release](https://github.com/reactwg/react-18/discussions/112).

![homepage](docs/media/homepage.png)
_Homepage_

![HN](docs/media/hn.png)
_HN_

**Benchmark specs:**

- React version: 18.0.0-beta-0cc724c77-20211125
- Next.js version: 12.0.4 (stable)
- Build: optimized for production
- Chrome-based browser
- Network connection: local
- Test device: desktop and mobile

We will use Lighthouse for benchmarking:

1. React Server Components (RSC) with HTTP streaming
2. Static + Client Side Rendering (CSR) without HTTP streaming

### React Server Components (RSC) with HTTP streaming

**Device: mobile**

![Lighthouse - RSC mobile](docs/media/rsc_mobile.png)
_Lighthouse_

![Original trace - RSC mobile](docs/media/rsc_mobile_perf_trace.png)
_Original trace_

**Device: desktop**

![Lighthouse - RSC desktop](docs/media/rsc_desktop.png)
_Lighthouse_

![Original trace - RSC desktop](docs/media/rsc_desktop_perf_trace.png)
_Original trace_

### Static + Client Side Rendering (CSR) without HTTP streaming

**Device: mobile**

![Lighthouse - CSR mobile](docs/media/csr_mobile.png)
_Lighthouse_

![Original trace - CSR mobile](docs/media/csr_mobile_perf_trace.png)
_Original trace_

**Device: desktop**

![Lighthouse - CSR desktop](docs/media/csr_desktop.png)
_Lighthouse_

![Original trace - CSR desktop](docs/media/csr_desktop_perf_trace.png)
_Original trace_
