# SDL2 for BL
Experimental SDL2 wrapper for BL.

# Installation
## Linux
Clone the repository into to the `bl` API folder.
```bash
cd $(blc -where-is-api)
git clone https://github.com/travisdoor/bl-sdl2.git sdl2
```
Install `SDL2` development package with your favorite package manager.
```bash
apt install libsdl2-dev
```

## macOS
Clone the repository into to the `bl` API folder.
```bash
cd $(blc -where-is-api)
git clone https://github.com/travisdoor/bl-sdl2.git sdl2
```
Install `SDL2` development package with your favorite package manager.
```bash
brew install sdl2
```

# Example
Minimal SDL2 application.
```rust
#import "sdl2"

TITLE :: "SDL2";
SCREEN_WIDTH :: 800;
SCREEN_HEIGHT :: 600;

main :: fn () s32 {
    if SDL_Init(SDL_INIT_VIDEO) != 0 { panic("Unable to init SDL"); }
    defer SDL_Quit();
    window :: SDL_CreateWindow(
        TITLE.ptr,
        100,
        100,
        SCREEN_WIDTH,
        SCREEN_HEIGHT,
        SDL_WINDOW_SHOWN
    );
    defer SDL_DestroyWindow(window);
    if !window {
        panic("Cannot create window.");
    }
    renderer :: SDL_CreateRenderer(window, -1, SDL_RENDERER_SOFTWARE);
    defer SDL_DestroyRenderer(renderer);
    if !renderer {
        panic("Cannot create renderer.");
    }
    SDL_SetRenderDrawColor(renderer, 0, 0, 0, 255);

    will_quit := false;
    loop !will_quit {
        os_sleep_ms(16.);
        event: SDL_Event;
        loop SDL_PollEvent(&event) != 0 {
            will_quit = event.type == SDL_EventType.QUIT;
        }
    }
    return 0;
};
```