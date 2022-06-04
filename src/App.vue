<template>
  <div class="container">
    <h3>Alışveriş Listesi</h3>
    <hr>
    <AddSection class="my-2" inputplaceholder="Ne Alacaksın" />
    <ListSection />
  </div>
</template>

<script>
  import axios from "axios";
  import ListSection from "@/components/ListSection";
  import AddSection from "@/components/AddSection";
  
  export default{
    components: {
      ListSection,
      AddSection,
    },
    data(){
      return {
        provideData: {
          itemList: [],
        },
      }
    },
    provide(){
      return{
        $itemList: () => this.provideData.itemList,
        onSave: this.onSave,
        onDelete: this.onDelete,
      }
    },
    mounted(){
      axios.get("http://localhost:3000/items").then(items_response => {
        console.log("response :" + JSON.stringify(items_response));
        this.provideData.itemList = items_response.data || [];
      });
    },
    methods: {
      onSave(e){
        if(e.target.value == ""){
          alert("Eklenecek değer boş olmamalıdır.");
          return;
        }
        const saveObject = {
          title: e.target.value,
          created_At: new Date(),
          completed: false
        };

        axios.post("http://localhost:3000/items", saveObject).then(save_response => {
          this.provideData.itemList.push(save_response.data);
          e.target.value = "";
          e.target.focus();
        });
      },
      onDelete(item){
        axios.delete(`http://localhost:3000/items/${item.id}`)
        .then(delete_response => {
          this.provideData.itemList = this.provideData.itemList.filter(x=>x.id !== item.id);
        });
      },
    },
  };
</script>