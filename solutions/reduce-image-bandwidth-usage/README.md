# Reduce next/image bandwidth usage

This example shows how to reduce bandwidth and processing costs using the `sizes` prop when using layout `fill`.

## Explanation

Using [`layout=fill`](https://nextjs.org/docs/api-reference/next/image#layout) in `next/image` is one of the most common patterns as it lets us use responsive parents and (along with the [`objectFit`](https://nextjs.org/docs/api-reference/next/image#objectfit) prop) our images will resize to it perfectly. But this leads to a common problem; as we don't know how large our parent might be, we can't serve an optimized image.

Consider the UI of our [demo](https://solutions-reduce-image-bandwidth-usage.vercel.sh):

![00](./public/docs/screenshot-0.png)
> A grid of cards where every card has a thumbnail

Our thumbnail is represented by this code:
```tsx
<Image layout="fill" src={card.thumbnail} alt={card.title} />
```

But wait, given this code we end up with this 👇

![01](./public/docs/screenshot-1.png)
> Our element has a width of 256px but we are serving a 1000px image!

The [`sizes`](https://nextjs.org/docs/api-reference/next/image#sizes) prop provides information about how wide the image will be at different breakpoints when using `layout="responsive"` or `layout="fill"`. In this case our grid limits the width of the card to a maximum of `320px`. So if we update our code to use sizes like this:
```tsx
<Image layout="fill" sizes="320px" src={card.thumbnail} alt={card.title} />
```

![02](./public/docs/screenshot-2.png)
> Now we are being served with an optimized image.

We also have a lot of images available for different viewport sizes that will be generated (and cached) on demand just when needed. By default, a variant will be available for every [`device size`](https://nextjs.org/docs/api-reference/next/image#device-sizes) configured. But we can also specify [`image sizes`](https://nextjs.org/docs/api-reference/next/image#image-sizes) that will be concatenated to the variants generated by device sizes when using `layout="responsive"` or `layout="fill"`.

## Demo

https://solutions-reduce-image-bandwidth-usage.vercel.sh

## How to Use

You can choose from one of the following two methods to use this repository:

### One-Click Deploy

Deploy the example using [Vercel](https://vercel.com?utm_source=github&utm_medium=readme&utm_campaign=next-example):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/git/external?repository-url=https://github.com/vercel/examples/tree/main/solutions/reduce-image-bandwidth-usage&project-name=reduce-image-bandwidth-usage&repository-name=reduce-image-bandwidth-usage)

### Clone and Deploy

Execute [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) with [npm](https://docs.npmjs.com/cli/init) or [Yarn](https://yarnpkg.com/lang/en/docs/cli/create/) to bootstrap the example:

```bash
npx create-next-app --example https://github.com/vercel/examples/tree/main/solutions/reduce-image-bandwidth-usage reduce-image-bandwidth-usage
# or
yarn create next-app --example https://github.com/vercel/examples/tree/main/solutions/reduce-image-bandwidth-usage reduce-image-bandwidth-usage
```

Next, run Next.js in development mode:

```bash
npm install
npm run dev

# or

yarn
yarn dev
```

Deploy it to the cloud with [Vercel](https://vercel.com/new?utm_source=github&utm_medium=readme&utm_campaign=edge-middleware-eap) ([Documentation](https://nextjs.org/docs/deployment)).
