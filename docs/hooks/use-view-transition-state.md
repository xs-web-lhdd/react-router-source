---
title: unstable_useViewTransitionState
---

# `unstable_useViewTransitionState`

<details>
  <summary>Type declaration</summary>

```tsx
declare function unstable_useViewTransitionState(
  to: To,
  opts: { relative?: "route" : "path" } = {}
): boolean;

type To = string | Partial<Path>;

interface Path {
  pathname: string;
  search: string;
  hash: string;
}
```

</details>

This hook returns `true` when there is an active [View Transition][view-transitions] to the specified location. This can be used to apply finer-grained styles to elements to further customize the view transition. This requires that view transitions have been enabled for the given navigation via the [unstable_viewTransition][link-view-transition] prop on the `Link` (or the `Form`, `navigate`, or `submit` call).

Consider clicking on an image in a list that you need to expand into the hero image on the destination page:

```jsx
function NavImage({ src, alt, id }) {
  let to = `/images/${idx}`;
  let vt = unstable_useViewTransitionState(href);
  return (
    <Link to={to} unstable_viewTransition>
      <img
        src={src}
        alt={alt}
        style={{
          viewTransitionName: vt ? "image-expand" : "",
        }}
      />
    </Link>
  );
}
```

[link-view-transition]: ../components/link#unstable_viewtransition
[view-transitions]: https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API
