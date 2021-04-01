# webgl-in-svg
Render shaders inside SVGs

![](./hello-world.svg)
<img src="./hello-world.svg">


## Uniforms
`uResolution` and `uTime` are included by default.
```
  <uniform name="uMouse" type="VEC_2" x="0.5" y="0.5"/>
  <uniform name="uColor" type="VEC_4" x="0" y="0" z="0" w="0"/>
```

## Shaders
```
  <vertex>
          precision mediump float;

          attribute vec3 aBaseVertexPosition;
          void main() {
                  gl_Position = vec4(aBaseVertexPosition, 1.0);
          }
  </vertex>
  <fragment>
          #ifdef GL_ES
          precision mediump float;
          #endif

          uniform vec2 uResolution;
          uniform float uTime;

          uniform vec2 uMouse;
          uniform vec4 uColor;

          float circle(vec2 st, vec2 center, float radius) {
                  return step(distance(st, center), radius);
          }

          void main() {
                  vec2 st = gl_FragCoord.xy / uResolution;
                  float circle = circle(st, uMouse, 0.25);
                  vec4 background = vec4(st, 0.5, 1.0);
                  vec4 foreground = uColor;
                  gl_FragColor = mix(background, foreground, circle);
          }
  </fragment>
```
