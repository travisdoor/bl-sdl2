# SDL2 for BL
Experimental SDL2 wrapper for BL.

# Installation
## Windows

Clone the repository into the `bl` API folder. Use `blc --where-is-api` to get correct path.
```bash
cd path/to/api
git clone https://github.com/travisdoor/bl-sdl2.git sdl2
```

## Linux

Clone the repository into to the `bl` API folder.
```bash
cd $(blc --where-is-api)
git clone https://github.com/travisdoor/bl-sdl2.git sdl2
```
Install `SDL2` development package with your favorite package manager.
```bash
apt install libsdl2-dev
```

## macOS
Clone the repository into to the `bl` API folder.
```bash
cd $(blc --where-is-api)
git clone https://github.com/travisdoor/bl-sdl2.git sdl2
```
Install `SDL2` development package with your favorite package manager.
```bash
brew install sdl2
```

# Example
Minimal SDL2 application in `example` folder. Use `blc -b` to compile.
```rust
#import "sdl2"

TITLE :: "SDL2";
SCREEN_WIDTH :: 800;
SCREEN_HEIGHT :: 600;

main :: fn () s32 {
    if Sdl.Init(Sdl.INIT_VIDEO) != 0 { panic("Unable to init SDL"); }
    defer Sdl.Quit();
    window :: Sdl.CreateWindow(
        TITLE.ptr,
        100,
        100,
        SCREEN_WIDTH,
        SCREEN_HEIGHT,
        Sdl.WINDOW_SHOWN
    );
    defer Sdl.DestroyWindow(window);
    if !window {
        panic("Cannot create window.");
    }
    renderer :: Sdl.CreateRenderer(window, -1, Sdl.RENDERER_SOFTWARE);
    defer Sdl.DestroyRenderer(renderer);
    if !renderer {
        panic("Cannot create renderer.");
    }
    Sdl.SetRenderDrawColor(renderer, 0, 0, 0, 255);

    will_quit := false;
    loop !will_quit {
        os_sleep_ms(16.);
        event: Sdl.Event;
        loop Sdl.PollEvent(&event) != 0 {
            will_quit = event.type == Sdl.EventType.QUIT;
        }
    }
    return 0;
};
```
