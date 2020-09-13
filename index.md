## TOON SHADER

We will go over how to create a toon shader

### Markdown

The following containts the fragment shader code

```markdown
#ifdef GL_ES
precision highp float;
#endif

uniform float time;
uniform vec2 u_resolution;
uniform vec2 mouse;
uniform vec3 spectrum;

uniform sampler2D texture0;
uniform sampler2D texture1;
uniform sampler2D texture2;
uniform sampler2D texture3;
uniform sampler2D prevFrame;
uniform sampler2D prevPass;
uniform sampler2D u_picture;

varying vec3 v_normal;
varying vec2 v_texcoord;

vec3 makeSquare(float size, vec2 st)
    {
        float leftbar = step(size, st.x);
        float rightbar = step(size, 1.0 - st.x);
        float topbar = step(size, st.y);
        float bottombar = step(size, 1.0 - st.y);
        return vec3(leftbar*rightbar*topbar*bottombar);
    }

vec2 getst()
    {
        return gl_FragCoord.xy/u_resolution.xy;
    }
        
void main(void)
{

    
    
    vec2 st = getst();
    //vec3 square = makeSquare(sin(time), st);
    float xzone = smoothstep(0.0, 1.0, st.x);//gradient on X
    //float yzone = smoothstep(0.0, 1.0, st.y);//gradient on Y
    
    vec4 pictureColor = texture2D(u_picture, vec2(v_texcoord.x, (1.0-v_texcoord.y)));
    pictureColor.rgb = floor(pictureColor.rgb*5.0)/5.0;
    gl_FragColor = vec4(pictureColor.rgb, 1.0);
}
```

