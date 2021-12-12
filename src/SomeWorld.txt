// Vertex shader program
var VSHADER_SOURCE =
	'attribute vec4 a_Position;\n' +
  	'attribute vec4 a_Color;\n' +
  	'uniform mat4 u_ViewMatrix;\n' +
	'uniform mat4 u_ProjMatrix;\n' +
	'uniform mat4 u_ModelMatrix;\n' +
	'uniform mat4 u_GlobalRotation;\n' +
  	'varying vec4 v_Color;\n' +
	'attribute vec2 vertTexCoord; \n' +
	'varying vec2 fragTexCoord; \n' +
  	'void main() {\n' +
  	'  gl_Position =  u_ProjMatrix *u_ViewMatrix * u_GlobalRotation * u_ModelMatrix * a_Position;\n' +
	'  v_Color = a_Color;\n' +
	'  fragTexCoord = vertTexCoord;\n' +
  	'}\n';

// Fragment shader program
var FSHADER_SOURCE =
  	'#ifdef GL_ES\n' +
  	'precision mediump float;\n' +
  	'#endif\n' +
  	'varying vec4 v_Color;\n' +
	'varying vec2 fragTexCoord;\n' +
	'uniform sampler2D sampler;\n' +
  	'void main() {\n' +
  	'  gl_FragColor = v_Color + texture2D(sampler, fragTexCoord);\n' +
  	'}\n';



//------------------sliders to rotate model -------------------------------
var cameraSlider = document.getElementById("cameraRange");
camera = 0;
cameraSlider.oninput = function() {
   	camera = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var perspectiveSlider = document.getElementById("perspectiveRange");
perspective = 45;
perspectiveSlider.oninput = function() {
   	perspective = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var xSlider = document.getElementById("xRange");
angleX = xSlider.value;
xSlider.oninput = function() {
   	angleX = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var ySlider = document.getElementById("yRange");
angleY = ySlider.value;
ySlider.oninput = function() {
   	angleY = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var zSlider = document.getElementById("zRange");
angleZ = zSlider.value;
zSlider.oninput = function() {
   	angleZ = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}
//----------------------------------------------------------------------

//------------------sliders to move camera -------------------------------
var camxSlider = document.getElementById("camxRange");
camX = camxSlider.value;
camxSlider.oninput = function() {
   	camX = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var camySlider = document.getElementById("camyRange");
camY = camySlider.value;
camySlider.oninput = function() {
   	camY = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}

var camzSlider = document.getElementById("camzRange");
camZ = camzSlider.value;
camzSlider.oninput = function() {
   	camZ = this.value;

	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

	renderScene();
}
//----------------------------------------------------------------------


function main() {
  	// Retrieve <canvas> element
  	canvas = document.getElementById('webgl');

  	// Get the rendering context for WebGL
  	gl = getWebGLContext(canvas);
  	if (!gl) {
    		console.log('Failed to get the rendering context for WebGL');
    		return;
  	}


  	// Initialize shaders
  	if (!initShaders(gl, VSHADER_SOURCE, FSHADER_SOURCE)) {
    		console.log('Failed to intialize shaders.');
    		return;
  	}


	// Set clear color and enable hidden surface removal
  	gl.clearColor(0.0, 0.0, 0.0, 1.0);
  	gl.enable(gl.DEPTH_TEST);

	// Clear color and depth buffer
  	gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

//----------------------building the owl --------------------------------------//


	renderScene();

//-----------------------------------------------------------------------------//
}

function renderScene(){

	//translate, rotate, scale

//----------------------------- Cubes ------------------------------------//
	var colors = new Float32Array([
   		 -1.0, 1.0, -1.0,   0, 0,
		-1.0, 1.0, 1.0,    0, 1,
		1.0, 1.0, 1.0,     1, 1,
		1.0, 1.0, -1.0,    1, 0,

		// Left
		-1.0, 1.0, 1.0,    0, 0,
		-1.0, -1.0, 1.0,   1, 0,
		-1.0, -1.0, -1.0,  1, 1,
		-1.0, 1.0, -1.0,   0, 1,

		// Right
		1.0, 1.0, 1.0,    1, 1,
		1.0, -1.0, 1.0,   0, 1,
		1.0, -1.0, -1.0,  0, 0,
		1.0, 1.0, -1.0,   1, 0,

		// Front
		1.0, 1.0, 1.0,    1, 1,
		1.0, -1.0, 1.0,    1, 0,
		-1.0, -1.0, 1.0,    0, 0,
		-1.0, 1.0, 1.0,    0, 1,

		// Back
		1.0, 1.0, -1.0,    0, 0,
		1.0, -1.0, -1.0,    0, 1,
		-1.0, -1.0, -1.0,    1, 1,
		-1.0, 1.0, -1.0,    1, 0,

		// Bottom
		-1.0, -1.0, -1.0,   1, 1,
		-1.0, -1.0, 1.0,    1, 0,
		1.0, -1.0, 1.0,     0, 0,
		1.0, -1.0, -1.0,    0, 1,
  	]);

	

	//sky
	var m = new Matrix4();
	var textureThere = false;
	var individColor = new Array(0, 0, 1, 1);
	var texture = 'dirt-image';

	m.setScale(100, 100, 100);
	drawCube(m, colors, textureThere, individColor, texture);

	//ground
	m = new Matrix4();
	textureThere = false;
	individColor = new Array(0, 1, 0, 1);
	texture = 'dirt-image';
	var m1 = new Matrix4();
	m.setTranslate(0, -2.5, 0);
	m1.setScale(1000, 0, 1000);
	m.multiply(m1);
	drawCube(m, colors, textureThere, individColor, texture);


	//cube to be textured
	
	individColor = new Array(1, 1, 1, 1);
	textureThere = true;
	texture = 'dirt-image';
	var m = new Matrix4();
	m.setTranslate(1, -1, 1);
	drawCube(m, colors, textureThere, individColor, texture);

	
	individColor = new Array(1, 1, 1, 1);
	textureThere = true;
	texture = 'stone-image';
	var m = new Matrix4();
	m.setTranslate(-2, -1, 1);
	drawCube(m, colors, textureThere, individColor, texture);
	


//------------------------------------------------------------------------------//

}

//---------------Draw Cube with the transformation matrix, M, applied-------------

function drawCube(M, color, textOrColor, singleColor, textureImage){

	// Set the vertex coordinates and color
  	var n = initVertexBuffers(gl, color, textOrColor, singleColor, textureImage);
  	if (n < 0) {
    		console.log('Failed to set the vertex information');
    		return;
  	}


	//set view, proj, global rotation and model matrices

  	// Get the storage location of u_ViewMatrix
  	var u_ViewMatrix = gl.getUniformLocation(gl.program, 'u_ViewMatrix');
  	if (!u_ViewMatrix) { 
    		console.log('Failed to get the storage location of u_ViewMatrix');
    		return;
  	}
  	// Set the eye point and the viewing volume and push it to u_ViewMatrix
  	var viewMatrix = new Matrix4();
  	viewMatrix.lookAt(camX, camY, camZ, Math.cos(camera)*5 + camX, 0, Math.tan(camera)*5 + camZ, 0, 1, 0);
	gl.uniformMatrix4fv(u_ViewMatrix, false, viewMatrix.elements);

	// Get the storage location of u_GlobalRotation
  	var u_GlobalRotation = gl.getUniformLocation(gl.program, 'u_GlobalRotation');
  	if (!u_GlobalRotation) { 
    		console.log('Failed to get the storage location of u_GlobalRotation');
    		return;
  	}

	//set rotate for x y and z axis
  	globalRotation = new Matrix4();
	var globalRotation1 = new Matrix4();
	var globalRotation2 = new Matrix4();

	globalRotation.setRotate(angleX, 1, 0, 0);
	globalRotation1.setRotate(angleY, 0, 1, 0);
	globalRotation2.setRotate(angleZ, 0, 0, 1);

	globalRotation.multiply(globalRotation1);
	globalRotation.multiply(globalRotation2);
	gl.uniformMatrix4fv(u_GlobalRotation, false, globalRotation.elements);

	// Get the storage location of u_ProjMatrix
  	var u_ProjMatrix = gl.getUniformLocation(gl.program, 'u_ProjMatrix');
  	if (!u_GlobalRotation) { 
    		console.log('Failed to get the storage location of u_GlobalRotation');
    		return;
  	}
  	// Set the eye point and the viewing volume
  	var projMatrix = new Matrix4();
	projMatrix.setPerspective(perspective, 1, 0.1, 1000);
	gl.uniformMatrix4fv(u_ProjMatrix, false, projMatrix.elements);

	var u_ModelMatrix = gl.getUniformLocation(gl.program, 'u_ModelMatrix');
  	if (!u_ModelMatrix) { 
    		console.log('Failed to get the storage location of u_ModelMatrix');
    		return;
  	}
  	// Set the eye point and the viewing volume
  	var modelMatrix = M;
	gl.uniformMatrix4fv(u_ModelMatrix, false, modelMatrix.elements);


	
	gl.drawElements(gl.TRIANGLES, n, gl.UNSIGNED_BYTE, 0);
	

}

//------------------------------------------------------------------------

	
//--------------initializing buffers and storing gemoetry-----------------
function initVertexBuffers(gl, color, text, single, image) {
  	// Create a cube
  	//    v6----- v5
  	//   /|      /|
  	//  v1------v0|
  	//  | |     | |
  	//  | |v7---|-|v4
  	//  |/      |/
  	//  v2------v3
  	var verticesColors = color;

  	// Indices of the vertices
  	var indices = new Uint8Array([
    		// Top
		0, 1, 2,
		0, 2, 3,

		// Left
		5, 4, 6,
		6, 4, 7,

		// Right
		8, 9, 10,
		8, 10, 11,

		// Front
		13, 12, 14,
		15, 14, 12,

		// Back
		16, 17, 18,
		16, 18, 19,

		// Bottom
		21, 20, 22,
		22, 20, 23
 	]);

  	// Create a buffer object
  	var vertexColorBuffer = gl.createBuffer();
  	var indexBuffer = gl.createBuffer();
  	if (!vertexColorBuffer || !indexBuffer) {
    		return -1;
  	}

  	// Write the vertex coordinates and color to the buffer object
  	gl.bindBuffer(gl.ARRAY_BUFFER, vertexColorBuffer);
  	gl.bufferData(gl.ARRAY_BUFFER, verticesColors, gl.STATIC_DRAW);

  	var FSIZE = verticesColors.BYTES_PER_ELEMENT;


  	// Assign the buffer object to a_Position and enable the assignment
  	var a_Position = gl.getAttribLocation(gl.program, 'a_Position');
  	if(a_Position < 0) {
    		console.log('Failed to get the storage location of a_Position');
    		return -1;
  	}
  	gl.vertexAttribPointer(a_Position, 3, gl.FLOAT, false, FSIZE * 5, 0);
  	gl.enableVertexAttribArray(a_Position);



	//decide color or texture here
	var colorLoc = gl.getAttribLocation(gl.program, 'a_Color');
	if(colorLoc < 0) {
    		console.log('Failed to get the storage location of a_Color');
    		return -1;
  	}
	gl.disableVertexAttribArray(colorLoc);


  	// Assign the buffer object to a_Color and enable the assignment
  	var a_Texture = gl.getAttribLocation(gl.program, 'vertTexCoord');
  	if(a_Texture < 0) {
    		console.log('Failed to get the storage location of a_Texture');
    		return -1;
  	}
	gl.vertexAttribPointer(a_Texture, 2, gl.FLOAT, false, FSIZE * 5, FSIZE * 3);
	//making the texture
	var boxTexture = gl.createTexture();
	gl.bindTexture(gl.TEXTURE_2D, boxTexture);
	gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
	gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
	gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR);
	gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
	gl.texImage2D(gl.TEXTURE_2D, 0, gl.RGBA, gl.RGBA, gl.UNSIGNED_BYTE, document.getElementById(image));
	gl.bindTexture(gl.TEXTURE_2D, boxTexture);


	//textures are displayed
	//for tinted textures change the color in the if statement
	if(text == true){
		gl.enableVertexAttribArray(a_Texture);
		gl.vertexAttrib4f(colorLoc, 0, 0, 0, 1);
	}//colors are displayed
	else{
		gl.disableVertexAttribArray(a_Texture);
		gl.vertexAttrib4f(colorLoc, single[0], single[1], single[2], single[3]);

	}



  	// Write the indices to the buffer object
  	gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, indexBuffer);
  	gl.bufferData(gl.ELEMENT_ARRAY_BUFFER, indices, gl.STATIC_DRAW);

  	return indices.length;
}
//--------------------------------end--------------------------------------------