<template>
<!-- <div ref="container" style="height: 1000px; width: 1000px;"></div> -->
<div style="display: flex;">

    <div>
        <canvas style="height: 1000px; width: 1100px;" id="c"></canvas>
    </div>
    <v-fade-transition>
    <div v-if="cabinetInfo">
        <v-card style="position: absolute;" class="mx-auto" height="1000" width="350">
            <template v-slot:title>
                <span class="font-weight-black">Кабинет 105</span>
            </template>

            <v-card-text style="display: flex;flex-direction: column;">
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>
               <span style="margin-top: 10px;">Лялин Михаил Сергеевич (в офисе)</span>


            </v-card-text>
        </v-card>
    </div>
  </v-fade-transition>
</div>
</template>

<script setup>
import {
    ref,
    onMounted,
    defineEmits
} from 'vue'
import * as THREE from 'three'
import {
    GLTFLoader
} from 'three/addons/loaders/GLTFLoader.js';
import {
    OrbitControls
} from 'three/addons/controls/OrbitControls.js';
const container = ref(null)

import {
    FontLoader
} from 'three/addons/loaders/FontLoader.js';
import {
    TextGeometry
} from 'three/addons/geometries/TextGeometry.js';
import {
    Tween,
    Easing,
    update
} from '@tweenjs/tween.js';

onMounted(() => {
    initThreeJS(container.value)
})

defineProps({
    msg: String,
})

let cabinetInfo = ref(false)
let visibleRight = ref(false)
const emits = defineEmits(['cabinetInfo'])

function createMesh(geometry, material, x, y, z, name) {
    const mesh = new THREE.Mesh(geometry, material.clone())
    mesh.position.set(x, y, z)
    mesh.name = name;
    return mesh;
}

function initThreeJS() {
    const canvas = document.querySelector('#c');
    const renderer = new THREE.WebGLRenderer({
        antialias: true,
        alpha: true,
        canvas
    });

    renderer.setClearColor(0x000000, 0);

    const fov = 45;
    const aspect = 2; // the canvas default
    const near = 0.1;
    const far = 100;
    const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
    const raycaster = new THREE.Raycaster();
    const mouse = new THREE.Vector2();
    const controls = new OrbitControls(camera, canvas);
    controls.target.set(0, 0, 0);
    controls.update();

    const target = {
        x: 0,
        y: 0,
        z: 5
    };
    const newPosition = {
        x: 5,
        y: 5,
        z: 10
    };

    camera.position.set(0, 100, 20);

    const pointersMarker = new THREE.Group();
    const markerGeometry = new THREE.SphereGeometry(0.4, 64, 64);
    const markerMaterial = new THREE.MeshBasicMaterial({
        color: '#EDEDED',
    });

    
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 4, 6, 4, 'cab_510'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 7, 6, 4, 'cab_509'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 6, 6, 2, 'cab_509a'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -0.7, 6, 2, 'cab_511'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -2.4, 6, 2, 'cab_512'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -5, 6, 4, 'cab_513'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -8, 6, 5, 'cab_514'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -7, 6, 2, 'cab_514а'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -9, 6, 2, 'cab_514б'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -11, 6, 3, 'cab_515'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -14, 6, 2, 'cab_516'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -17, 6, 2, 'cab_517'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -15, 6, -2, 'cab_518'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -7.5, 6, -2, 'cab_519'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, -4, 6, -2, 'cab_599'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 0, 6, -2, 'cab_519'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 3, 6, -2, 'cab_598'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 5, 6, -2, 'cab_501'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 8, 6, -2, 'cab_502'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 12, 6, -2, 'cab_503'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 13.5, 6, -2, 'cab_504'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 16, 6, -2, 'cab_505'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 16, 6, 2, 'cab_506'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 12.5, 6, 2.5, 'cab_507'))
    pointersMarker.add(createMesh(markerGeometry, markerMaterial, 10, 6, 2.5, 'cab_508'))
   

    const hitboxGeometry = new THREE.BoxGeometry(100, 100, 100); // Увеличиваем размер хитбокса
    const hitboxMaterial = new THREE.MeshBasicMaterial({
        transparent: true,
        opacity: 0,

    });
    const hitbox = new THREE.Mesh(hitboxGeometry, hitboxMaterial);

    const loader = new FontLoader();
    loader.load('https://cdn.jsdelivr.net/npm/three@0.128.0/examples/fonts/helvetiker_regular.typeface.json', function (font) {
        // Создаем текст
        const textGeometry = new TextGeometry('1', {
            font: font,
            size: 30,
            height: 4,
            curveSegments: 12,
            bevelEnabled: true,
            bevelThickness: 0.2,
            bevelSize: 0.02,
            bevelOffset: 0,
            bevelSegments: 5
        });

        const textMaterial = new THREE.MeshBasicMaterial({
            color: '#7D7D7D'
        });
        const textMesh = new THREE.Mesh(textGeometry, textMaterial);

        // Размещаем текст на сфере
        textMesh.position.set(800, 250, -590); // Пример позиции на сфере
        //pointers.add(textMesh);
    });

    const pointersHitbox = new THREE.Group();
    pointersHitbox.add(createMesh(hitboxGeometry, hitboxMaterial, 800, 250, -600, 'marker1_hitbox'))
    pointersHitbox.add(createMesh(hitboxGeometry, hitboxMaterial, 600, 100, 100, 'marker2_hitbox'))

    window.addEventListener('click', function (event) {
        // Нормализация координат мыши
       mouse.x = ( ( event.clientX - renderer.domElement.offsetLeft ) / renderer.domElement.width ) * 2 - 1;
    mouse.y = - ( ( event.clientY - renderer.domElement.offsetTop ) / renderer.domElement.height ) * 2 + 1;

        // Обновление луча
        raycaster.setFromCamera(mouse, camera);

        // Проверка пересечений
        const intersects = raycaster.intersectObjects(pointersMarker.children, true);
      
        if (intersects.length > 0) {
            const intersect = intersects[0];
            cabinetInfo.value = !cabinetInfo.value
            console.log('Clicked on:', intersect.object);
            visibleRight.value = true
            const color = new THREE.Color('#4d4d4d')
            intersect.object.material.color = color
            emits('cabinetInfo', intersect.object)
        }
        else{
           
        }
    });

    window.addEventListener('mousemove', function (event){
        mouse.x = ( ( event.clientX - renderer.domElement.offsetLeft ) / renderer.domElement.width ) * 2 - 1;
        mouse.y = - ( ( event.clientY - renderer.domElement.offsetTop ) / renderer.domElement.height ) * 2 + 1;
        raycaster.setFromCamera(mouse, camera);

        const intersects = raycaster.intersectObjects(pointersMarker.children, true);

        if(intersects.length >0){
            document.documentElement.style.cursor = 'pointer'
            document.body.style.cursor = 'pointer';
        }
        else {
            document.documentElement.style.cursor = '';
            document.body.style.cursor = '';
        }
    })



    const scene = new THREE.Scene();

    {

        const skyColor = 0xB1E1FF;
        const groundColor = 0xB97A20; 
        const intensity = 2;
        const light = new THREE.HemisphereLight(skyColor, groundColor, intensity);
        scene.add(light);

    }

    {
        const color = 0xFFFFFF;
        const intensity = 2.5;
        const light = new THREE.DirectionalLight(color, intensity);
        light.position.set(5, 10, 2);
        scene.add(light);
        scene.add(light.target);
    }

    function frameArea(sizeToFitOnScreen, boxSize, boxCenter, camera) {

        const halfSizeToFitOnScreen = sizeToFitOnScreen * 1;
        const halfFovY = THREE.MathUtils.degToRad(camera.fov * .5);
        const distance = halfSizeToFitOnScreen / Math.tan(halfFovY);

        const direction = (new THREE.Vector3())
            .subVectors(camera.position, boxCenter)
            .multiply(new THREE.Vector3(1, 1, 3))
            .normalize();

        camera.position.copy(direction.multiplyScalar(distance).add(boxCenter));

        camera.near = boxSize / 200;
        camera.far = boxSize * 200;
        camera.updateProjectionMatrix();
        camera.lookAt(boxCenter.x, boxCenter.y, boxCenter.z);

    }

    {

        const gltfLoader = new GLTFLoader();
        gltfLoader.load('src/assets/test7.glb', (gltf) => {

            const root = gltf.scene;

            hitbox.position.set(800, 250, -600)
            // root.add(pointersHitbox);
            root.add(pointersMarker)
            //scene.add(pointers)
            scene.add(root);
            const box = new THREE.Box3().setFromObject(root);

            const boxSize = box.getSize(new THREE.Vector3()).length();
            const boxCenter = box.getCenter(new THREE.Vector3());
            frameArea(boxSize * 0.5, boxSize, boxCenter, camera);

            controls.maxDistance = boxSize * 10;
            controls.target.copy(boxCenter);
            controls.update();

        });

    }

    function resizeRendererToDisplaySize(renderer) {

        const canvas = renderer.domElement;
        const width = canvas.clientWidth;
        const height = canvas.clientHeight;
        const needResize = canvas.width !== width || canvas.height !== height;
        if (needResize) {

            renderer.setSize(width, height, false);

        }

        return needResize;

    }

    function render() {

        if (resizeRendererToDisplaySize(renderer)) {

            const canvas = renderer.domElement;
            update();
            camera.aspect = canvas.clientWidth / canvas.clientHeight;
            camera.updateProjectionMatrix();

        }

        renderer.render(scene, camera);

        requestAnimationFrame(render);

    }

    requestAnimationFrame(render);

}

// const initThreeJS = (container) => {
//       // Создание сцены
//       const scene = new THREE.Scene();
//       scene.background = new THREE.Color( 'gray' );
//       const mesh = new THREE.Mesh()
//       const loader = new GLTFLoader();
//       loader.load('src/assets/office_space.glb', function (gltf) {
//         scene.add(gltf.scene);

//       }, undefined, function(error){
//         console.error(error);
//       })

//       // Создание камеры
//       const camera = new THREE.PerspectiveCamera(50, container.clientWidth / container.clientHeight, 1, 10000);
//       camera.position.z = 50;
//       camera.position.y = 2;

//       const controls = new OrbitControls( camera, container );
// 	    controls.target.set( 0, 20, 0 );
// 	    controls.update();

//       // Создание рендерера
//       const renderer = new THREE.WebGLRenderer();
//       renderer.setSize(container.clientWidth, container.clientHeight);
//       container.appendChild(renderer.domElement);
//       const light = new THREE.DirectionalLight(0xffffff, 1);
//       light.position.set(10, 1, 1).normalize();
//       scene.add(light);

//       // Функция анимации
//       const animate = function () {
//         requestAnimationFrame(animate);
//       renderer.render(scene, camera);
//       };

//       // Запуск анимации
//       animate();
//     };
</script>

<style scoped>
.read-the-docs {
    color: #888;
}
</style>
