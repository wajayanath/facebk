<template>
    <div>
        <img src="https://i.pinimg.com/originals/ae/b4/40/aeb440b2d44f0d12315a14ec2316997d.jpg"
             alt="user background image"
             ref="userImage"
             class="object-cover w-full">
        <!--<img :src="imageObject.data.attributes.path"-->

    </div>
</template>

<script>
    import Dropzone from 'dropzone';

    export default {
        name: "UploadableImage",

        props: [
          // 'userImage',
          'imageWidth',
          'imageHeight',
          'location',

        ],
        //
        data:() => {
            return {
                dropzone: null,
                // uploadedImage: null,
            }
        },

        mounted() {
            this.dropzone = new Dropzone(this.$refs.userImage, this.settings);
        },
        //
        computed: {
            settings() {
                return {
                    paramName: 'image',
                    url: '/api/user-images',
                    acceptedFiles: 'image/*',
                    params: {
                        'width': this.imageWidth,
                        'height': this.imageHeight,
                        'location': this.location,
                    },
                    headers: {
                        'X-CSRF-TOKEN': document.head.querySelector('meta[name=csrf-token]').content,
                    },
                    success: (e, res) => {
                       // this.uploadedImage = res;
                        alert('uploaded');
                    }
                };
            },
        //     imageObject() {
        //         return this.uploadedImage || this.userImage;
        //     }
        }
    }
</script>

<style scoped>

</style>