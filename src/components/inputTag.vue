<script>
export default {
    emits:["OnTagsChange"],
    data() {
        return {
           currentValue: "",
            tags: [],
        }
    },
    methods: {
        handleKeyDown(e) {
            if (e.key === "Backspace" && this.currentValue === "" && this.tags.length > 0 ) {
                this.tags.pop();
                this.$emit("OnTagsChange", this.tags);
               // this.OnTagsChange(this.tags);
                //this.tags.push(this.currentValue); e.key === "Enter" && this.currentValue !== "" ? this.tags.push(this.currentValue) : "";
             //   this.currentValue = "";
            }
        },
        handleSubmit() {
            const exist = this.tags.find(tag => (tag === this.currentValue) );
            if (!exist && this.currentValue !== ""){
                this.tags.push(this.currentValue);
                //this.OnTagsChange(this.tags);
                this.$emit("OnTagsChange", this.tags);
            }
            
            this.currentValue = "";
        },
        deleteTag(index) {
            this.tags.splice(index, 1);
           // this.OnTagsChange(this.tags);
           this.$emit("OnTagsChange", this.tags);
        }
    }
}
</script>

<template>
    <div class="inputTag">
        <div class="tags"> 
            <div class="tag" v-for="(tag,index) in tags" :key="index">
                {{tag}} <button @click="deleteTag(index)">X</button>
            </div>
        </div>
        <form @submit.prevent="handleSubmit">
        <input class="input" type="text" v-model="currentValue" @keydown="handleKeyDown"   />
    </form>
    </div>
</template>

<style scoped>
.inputTag {
    display: flex;
    flex-direction: column;
    width: 300px;
    margin: 100px auto;
    padding: 10px;
    border: 1px solid #141313;
    border-radius: 5px;
}
.tags {
    display: flex;
    flex-wrap: wrap;
}
.tags .tag {
    background-color: #a0a0a0;
    padding: 5px;
    margin: 5px;
    border-radius: 5px;
}
.inputTag form {
    display: inline-flex;
}
.inputTag input {
    padding: 5px;
    margin-top: 10px;
    border: 1px solid #141313;
    border-radius: 5px;
}
.inputTag button {
    margin-left: 5px;
    background-color: #c0c0c0;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
.tag button:hover {
    margin-left: 5px;
    background-color: #ca1010;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
</style>