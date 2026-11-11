# Calculator

The Arche phone's calculator, written in [Arche](https://github.com/arche-family/arche-lang): a Nimadir mini-app, a WebAssembly component of Nimadir's world, which the phone installs from its repository and Nimadir runs on a desktop.

It works like Android's. What is typed is along the top, and what it comes to shows under it as it is typed. Below them is a 4×5 grid of keys, laid out as a CSS grid.

- Times and divide come before plus and minus, and brackets come first.
- A bracket left open is closed at the end.
- = puts the result in place of what was typed.
- Dividing by zero says "Can't divide by 0".
- Results show up to 12 significant digits, with an exponent when they do not fit.

It is an app of the page: its keys are DOM buttons, and their taps come as click events.

## Build

With [arche-lang](https://github.com/arche-family/arche-lang) checked out next to this repository and built (`make -C stage0 && make -C compiler && make -C wasm`):

```sh
../arche-lang/wasm/nimadir-app.sh . calculator.component.wasm
```

`manifest` is what the phone's repository packages with the component. It gives the app's name, version and title, and what it may do: nothing beyond its own screen.

## Test

`headless` holds the taps of a headless run, and `expected.txt` holds what Nimadir's own shell said to them. `app-check.sh` runs the app with arche-wasm, by the interpreter and by the JIT, and compares what it says with `expected.txt`. CI runs it on every push.

```sh
../arche-lang/wasm/app-check.sh .
NIMADIR=~/nimadir ../arche-lang/wasm/app-expected.sh .   # expected.txt again, from Nimadir's shell
```

## License

MIT or Apache-2.0, at your option ([LICENSE](LICENSE)).
