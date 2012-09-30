## keyboard

Keyboard is a package which offers a universal keyboard event interface
for various backends. The backends are implemented as separate packages.

This is based on ccampbell's javascript library [mousetrap][mt].

[mt]: https://github.com/ccampbell/mousetrap

Keybindings for an application are specified through a backend implementation.
Apart from individual keys, it can bind sequences on which events have
to be triggered.


### Examples

Creating a new keyboard (for GLFW in this case):

	import "github.com/jteeuwen/keyboard/glfw"
	...
	kb := glfw.New()

Binding a single key:

	kb.Bind(func() {
		println("'s' was pressed.")
	}, "s")

Binding a single key with modifier:

	kb.Bind(func() {
		println("'ctrl+s' was pressed.")
	}, "ctrl+s")

Binding a single key with multiple modifiers:

	kb.Bind(func() {
		println("'shift+ctrl+s' was pressed.")
	}, "shift+ctrl+s")

Binding multiple shortcuts to the same handler:

	kb.Bind(func() {
		println("'ctrl+s' or 'command+s' was pressed.")
	}, "ctrl+s", "command+s")

Binding a key sequence:

	kb.Bind(func() {
		println("Konami Code!")
	}, "up up down down left right left right b a enter")


### Sequences

A sequence binding is triggered by typing the letters in the sequence,
one after another. The package records all keypresses and triggers the
appropriate handler when a known sequence has been completed.

The recording is reset when a wrong character is typed, or one takes too
long to type followup characters. The timeout for these resets is configurable.


### Backends

A backend is implemented as a separate package which implements the `Keyboard`
interface defined in this package. If a backend requires initialization, the
host application is responsible for doing so before calling any of the keyboard
functions.

For instance, GLFW requires calling of some initialization functions which the
keyboard package can not do for you. Reason being that the initialization
may require information specific to the host application. It is therefore up
to the caller to do the setup first, then bind all the keys.
Refer to `glfw/keyboard_test.go` for an example of this.


### Usage

    go get github.com/jteeuwen/keyboard


### License

Unless otherwise stated, all of the work in this project is subject to a
1-clause BSD license. Its contents can be found in the enclosed LICENSE file.

