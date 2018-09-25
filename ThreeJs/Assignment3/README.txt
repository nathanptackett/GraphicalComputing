1) Shader Code
        <script id="vertexShader" type="x-shader/x-vertex">
            precision highp float;

            attribute vec3 position;

            uniform mat4 modelViewMatrix;
            uniform mat4 projectionMatrix;
            uniform mat3 normalMatrix;

            void main()	{
                gl_Position = projectionMatrix*modelViewMatrix*vec4(position, 1.0 );
            }
        </script>

        <script id="fragmentShader" type="x-shader/x-fragment">
            precision highp float;
            uniform int radius;
            uniform vec2 mousePos;
            uniform vec2 resolution;

            void main()	{
                gl_FragColor = vec4(mousePos.x/resolution.x, mousePos.y/resolution.y, mousePos.x/mousePos.y, 1.0);
            }
        </script>
2) The cube object has the shader material
3) File is Assignment3.html on lines 60-71 AND resetting the shader on mouse move on lines 85-96