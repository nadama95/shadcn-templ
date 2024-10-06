# Shadcn/ui port for Go + Templ + Alpine.js + Tailwind CSS

### Note

This is a work in proccess. 

- Not all the components from shadcn/ui are implemented.
- There are refinements needed for some of the components - alpine.js naming, unfinished accessibility, improvements I want to make, etc.
- Some components might contain behavior that existed for previous needs (I detached the developement of this from another project). Hopefully will be fixed in the future.

## Overview

A [shadcn/ui](https://ui.shadcn.com/) port using [Go](https://go.dev/), [Templ](https://templ.guide/), [Alpine.js](https://alpinejs.dev/) and [Tailwind CSS](https://tailwindcss.com/).

### Usage 

You have to include the [Head](https://github.com/rotemhoresh/shadcn-templ/blob/main/include.templ#L4) component in your `head` tag (it includes the neccessery scripts - HTMX, Alpine.js and a theme script).
You have to serve the [CSS](https://github.com/rotemhoresh/shadcn-templ/blob/main/css.go#L10) var and link to it in your `head` tag.

Example:

```go
router.HandleFunc("GET /static/css/styles.css", func(w http.ResponseWriter, r *http.Request) {
  w.Header().Set("Content-Type", "text/css")
  w.Write(shadcntempl.CSS)
})
```

```templ
templ Layout() {
  <!DOCTYPE html>
	<html lang="en">
		<head>
      // ...
      @shadcntempl.Head()
			<link rel="stylesheet" href="/static/css/styles.css"/>
      // ...
		</head>
		<body>
			{ children... }
		</body>
	</html>

}
```

### Example

Use in `.templ` files.

```templ
import "github.com/rotemhoresh/shadcn-templ/ui"

templ Page() {
  @ui.Button(ui.ButtonTypeButton, ui.ButtonVariantDefault, ui.ButtonSizeDefault, "additional-classes", templ.Attributes{}) {
    Click me
  }
}
```

### Design

The components props (parameters) is structures like this:

```templ
templ Comp(componentSpecificParams, classes string, attrs templ.Attributes)
```

Any **components specific parameters** at the begining, then **classes** and **attrs** for every component (see [example](#example) for the params of the `Button` component).

## Contributing

Contributions are welcome for both new components and improvements for existing ones.

Make sure to read the README.md and go over the codebase to understand the design choices and overall coding style.

### License 

MIT
