Shader code defined on line 88 and 119

      <script id="vertexShader" type="x-shader/x-vertex">
         precision highp float;

         attribute vec3 position;
         attribute vec2 uv;
         varying vec2 vUV;

         attribute vec3 normal;
         varying vec3 vNormal;

         uniform mat4 modelViewMatrix;
         uniform mat4 projectionMatrix;
         varying vec4 vPosition;
         uniform mat3 normalMatrix;

         void main() {
            vUV = uv;
            vNormal = normalize(normal);
            gl_Position = projectionMatrix*modelViewMatrix*vec4(position, 1.0);
            vPosition = gl_Position;
         }
      </script>

      <script id="fragmentShader" type="x-shader/x-fragment">
         precision highp float;

         uniform float light_intensity;
         uniform vec3 light_color;
         uniform vec3 light_position;
         uniform vec3 material_color;
         uniform sampler2D texture;
         varying vec3 vNormal;
         varying vec2 vUV;
         varying vec4 vPosition;

         void main() {
            vec4 color = texture2D(texture, vUV);
            vec3 vector_to_light_position = light_position - vPosition.xyz;
            vector_to_light_position = normalize(vector_to_light_position);

            float cos_of_angle_between = dot(vNormal, vector_to_light_position);

            gl_FragColor = vec4(light_intensity*cos_of_angle_between, 1);
         }
      </script>
