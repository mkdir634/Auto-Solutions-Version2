<template>
    <v-row class="model-viewer-container">
        <model-viewer src="/models/toyota_supra.glb" ar ar-modes="webxr scene-viewer quick-look" tone-mapping="neutral"
            poster="poster.webp" shadow-intensity="1.4" camera-orbit="-300deg 80deg 4m"
            min-camera-orbit="auto auto 4.911m" max-camera-orbit="auto 100deg 9m" min-field-of-view="12deg"
            ref="modelViewer" >

            <button id="tires" class="hotspot" slot="hotspot-1"
                data-position="-0.8591577229878414m 0.2675076114826115m 1.414183157525556m"
                data-normal="-0.008226973476527363m 0.6343190777223924m -0.7730275703652684m"
                data-visibility-attribute="visible"
                @click="zoomToHotspot('36.78414m 98.2675076114826115m 5.414183157525556m')">
                <div class="hotspot-annotation"></div>
            </button>
            <button id="back" class="hotspot" slot="hotspot-3"
                data-position="-0.017936046896674565m 0.6817013441585476m -1.9770060065888153m"
                data-normal="-0.006273411558989916m 0.2869887537758104m -0.9579134091939724m"
                data-visibility-attribute="visible"
                @click="zoomToHotspot('180.78414m 89.2675076114826115m 10.4525556m')">
                <div class="hotspot-annotation"></div>
            </button>
            <button id="interior" class="hotspot" slot="hotspot-4"
                data-position="0.6765970783473938m 1.011742867066152m -0.0439240954590262m"
                data-normal="0.9009793442485632m 0.433575908717354m 0.01575286060846306m"
                data-visibility-attribute="visible" @click="zoomToHotspot('230.6deg 78.33m -1.04m')">
                <div class="hotspot-annotation"></div>
            </button>
            <button id="body" class="hotspot" slot="hotspot-5"
                data-position="0.6799885454498241m 0.5826037127122909m 1.959285014032719m"
                data-normal="0.46335479226336795m 0.6328190420284213m 0.6203566688065846m"
                data-visibility-attribute="visible" @click="zoomToHotspot('340deg 85m 10.959285014032719m')">
                <div class="hotspot-annotation"></div>
            </button>
            <div class="progress-bar hide" slot="progress-bar">
                <div class="update-bar"></div>
            </div>

            <div class="container-fluid">
                <div class="row">
                    <div class="col">
                        <button class="custom-button ms-1 mt-3" @click="BodyButton">
                            <router-link to="/Home" class="nav-link" >HOME</router-link>
                        </button>
                        <button class="custom-drpdown ms-1 mt-3 dropdown-toggle" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            MENU
                        </button>
                        <ul class="dropdown-menu">
                            <li><router-link to="/Honda" class="dropdown-item" >2024 HONDA CIVIC</router-link></li>
                            <li><router-link to="/Nissan" class="dropdown-item" >2024 NISSAN Z PERFORMANCE</router-link>
                            </li>
                        </ul>

                        <h1 class="headertext">Auto-Solutions</h1>
                    </div>
                    <div class="col mt-3 me-10 d-flex justify-content-end">
                        <button class="custom-button me-2 my-auto d-flex"> <v-icon class="me-1 my-auto">mdi-shopping</v-icon> PURCHASE</button>
                        <button class="custom-button ms-2" @click="BodyButton">BODY</button>
                        <button class="custom-button ms-2" @click="BackButton">BACK</button>
                        <button class="custom-button ms-2" @click="TireButton">TIRES</button>
                        <button class="custom-button ms-2" @click="InteriorButton">INTERIOR</button>
                        <button class="custom-button" @click="modalBody = true" style="display: none;">Open
                            Modal</button>
                    </div>
                </div>

                <div v-if="modalBody" class="modal-overlay">
    <div class="card modal-card-body"
       >
        <div class="card-body">
            <h5 class="card-title">Card Title</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk
                of the card's content.</p>
            <a href="#" class="btn btn-primary" @click="closeModal">Go somewhere</a>
        </div>
    </div>
</div>


                <div v-if="modalTire" class="modal-overlay">
                    <div class="card"
                        style="width: 20rem; background: rgba(255, 255, 255, 0.9); border: none; margin-top: 10%; margin-left: auto; margin-right: 65%;">
                        <div class="card-body">
                            <h5 class="card-title">Card Title</h5>
                            <p class="card-text">Some quick example text to build on the card title and make up the bulk
                                of the card's content.</p>
                            <a href="#" class="btn btn-primary" @click="closeModal">Go somewhere</a>
                        </div>
                    </div>
                </div>

                <div v-if="modalBack" class="modal-overlay">
                    <div class="card"
                        style="width: 20rem; background: rgba(255, 255, 255, 0.9); border: none; margin-top: 2%; margin-left: auto; margin-right: 75%;">
                        <div class="card-body">
                            <h5 class="card-title">Card Title</h5>
                            <p class="card-text">Some quick example text to build on the card title and make up the bulk
                                of the card's content.</p>
                            <a href="#" class="btn btn-primary" @click="closeModal">Go somewhere</a>
                        </div>
                    </div>
                </div>

                <div v-if="modalInterior" class="modal-overlay">
                    <div class="card modal-card-Interior"
                        style="">
                        <div class="card-body">
                            <h5 class="card-title">Card Title</h5>
                            <p class="card-text">Some quick example text to build on the card title and make up the bulk
                                of the card's content.</p>
                            <a href="#" class="btn btn-primary" @click="closeModal">Go somewhere</a>
                        </div>
                    </div>
                </div>


            </div>
        </model-viewer>
    </v-row>
</template>

<script>
import { useRouter } from 'vue-router';

export default {
    name: 'ModelViewerComponent',
    data() {
        return {
            cameraOrbit: 'auto auto 6m',
            fieldOfView: '15.4deg',
            modalBody: false,
            modalTire: false,
            modalBack: false,
            modalInterior: false,
        };
    },
    methods: {
        updateCamera(event) {
            const modelViewer = this.$refs.modelViewer;
            if (modelViewer) {
                this.cameraOrbit = modelViewer.cameraOrbit;
                this.fieldOfView = modelViewer.fieldOfView;
            }
        },
        zoomToHotspot(position) {
            const modelViewer = this.$refs.modelViewer;
            const [x, y, z] = position.split(' ').map(val => parseFloat(val));

            // Smoothly zoom in and move camera to the hotspot position
            if (modelViewer) {
                modelViewer.cameraOrbit = `-${x}deg ${y}deg ${z}m`;
                modelViewer.fieldOfView = '10deg';
                modelViewer.cameraTarget = `${x} ${y} ${z}`;
            }
        },
        BodyButton() {
            // Trigger a click on the BODY button
            const bodyButton = document.getElementById('body');
            if (bodyButton) {
                this.closeModal();
                bodyButton.click();

                // After 1-second delay, trigger the modal button click
                setTimeout(() => {
                    this.modalBody = true;
                }, 500); // 1000ms = 1 second
            }
        },
        BackButton() {
            const bodyButton = document.getElementById('back');
            if (bodyButton) {
                this.closeModal();
                bodyButton.click();

                setTimeout(() => {
                    this.modalBack = true;
                }, 500);
            }
        },
        InteriorButton() {
            const bodyButton = document.getElementById('interior');
            if (bodyButton) {
                this.closeModal();
                bodyButton.click();

                setTimeout(() => {
                    this.modalInterior = true;
                }, 500);
            }
        },
        TireButton() {
            const bodyButton = document.getElementById('tires');
            if (bodyButton) {
                this.closeModal();
                bodyButton.click();

                setTimeout(() => {
                    this.modalTire = true;
                }, 500); // 1000ms = 1 second
            }
        },
        closeModal() {
            this.modalBody = false;
            this.modalTire = false;
            this.modalBack = false;
            this.modalInterior = false;
        },
        handleButtonClick() {
            this.closeModal(); // Close modal when any button is clicked
        }
    },
    mounted() {
        const modelViewer = this.$refs.modelViewer;
        if (modelViewer) {
            modelViewer.addEventListener('camera-change', this.updateCamera);
        }
    },
    beforeDestroy() {
        const modelViewer = this.$refs.modelViewer;
        if (modelViewer) {
            modelViewer.removeEventListener('camera-change', this.updateCamera);
        }
    }
};
</script>


<style>
.model-viewer-container {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100vh;
    background: radial-gradient(circle, #ffffff, #f7b367);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    margin: 0;
    padding: 0;
    overflow: hidden;
}

model-viewer {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
}

.hotspot {
    display: none;
}



.progress-bar {
    position: absolute;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    width: 80%;
    height: 5px;
    background: rgba(0, 0, 0, 0.2);
    border-radius: 5px;
}

.update-bar {
    height: 100%;
    background: #007bff;
    width: 0%;
    border-radius: 5px;
}

.headertext {
    color: #151515;
    position: absolute;
    font-size: 180px;
    z-index: -1;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -98%);
    white-space: nowrap;
    pointer-events: none;
}

@media only screen and (max-width: 1024px) {
    .headertext {
        font-size: 120px;
        top: 35%;
        transform: translate(-50%, -90%);
    }
}

@media only screen and (max-width: 768px) {
    .headertext {
        font-size: 80px;
        top: 30%;
        transform: translate(-50%, -85%);
    }
}

@media only screen and (max-width: 480px) {
    .headertext {
        font-size: 60px;
        top: 25%;
        transform: translate(-50%, -80%);
    }
}

.custom-button {
    color: #151515;
    text-decoration: none;
    font-size: 15px;
    border: none;
    background: none;
    font-weight: 600;
    font-family: 'Poppins', sans-serif;
}
.custom-drpdown {
    color: #151515;
    text-decoration: none;
    font-size: 15px;
    border: none;
    background: none;
    font-weight: 600;
    font-family: 'Poppins', sans-serif;
}

.custom-button::before,
.custom-button::after {
    content: '';
    width: 0%;
    height: 2px;
    background: rgba(255, 0, 0, 0.5);
    display: block;
    transition: 0.5s;
}

.custom-button:hover::after,
.custom-button:hover::before {
    width: 100%;
}

.close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 20px;
    cursor: pointer;
}

.btn-close {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    font-size: 1.25rem;
    color: #000;
}

.card-body {
    color: #000;
}

.modal-card-body {
width: 20rem; background: rgba(255, 255, 255, 0.9); border: none; margin-top: 20%; margin-left: 75%; margin-right: auto;
}
.modal-card-Interior{
    width: 20rem; background: rgba(255, 255, 255, 0.9); border: none; margin-top: 15%; margin-left: 60%; margin-right: auto;

}

/* small screen */
@media (max-width: 768px) {
    .modal-card-body {
        position: fixed;
        top: 78%;
        left: 50%;
        transform: translate(-50%, -50%);
        margin: 0; /* Override the original margins */
    }
    .modal-card-Interior {
        position: fixed;
        top: 78%;
        left: 50%;
        transform: translate(-50%, -50%);
        margin: 0; /* Override the original margins */
    }
}
</style>