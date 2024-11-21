<template>
    <base-card>
    <!-- Keep in mind here that we are putting an event on the component and this click event will fall on the <button> inside the component -->
        <base-button 
            @click="setSelectedTab('stored-resources')"
            :mode="storedResButtonMode">Stored resources
        </base-button>

        <base-button 
            @click="setSelectedTab('add-resource')"
            :mode="addResButtonMode"
            >Add resource
        </base-button>
    </base-card>

    <!-- Here we'll "inject" the 'html tag' of our custom components: stored-resources || add-resource -->
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>  
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';

    export default {
        components: {
            StoredResources,
            AddResource
        },
        data() {
            return {
                selectedTab: 'stored-resources',
                storeResources: [
                {
                    id: 'official-giude',
                    tittle: 'Oficial Guide',
                    description: 'The official Vue JS Documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    tittle: 'Google',
                    description: 'The official Internet search site',
                    link: 'https://www.google.com'
                },
            ]
            }
        },
        provide() {
            return {
                resources: this.storeResources,
                addResource: this.addResource
            }
        },  
        computed: {
            storedResButtonMode() {
                return this.selectedTab === 'stored-resources' ? null : 'flat'
            },
            addResButtonMode() {
                return this.selectedTab === 'add-resource' ? null : 'flat'
            }
        },
        methods: {
            setSelectedTab(tab) {
                this.selectedTab = tab
            },
            addResource(title, description, url) {
                const newResource = {
                    id: new Date().toISOString(),
                    title: title,
                    description: description,
                    link: url
                }
                // Isso colocaria ele no array, normalmente
                // this.storeResources.push(newResource)

                // Aqui colocamos o objeto no topo do array
                this.storeResources.unshift(newResource)
                this.selectedTab = 'stored-resources'
            }
        }
    }
</script>