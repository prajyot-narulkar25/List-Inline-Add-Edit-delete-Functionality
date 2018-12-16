<template>
  <div class="hello">

    <div class="container">
    <div class="row pb-2">
        <div class="col-sm-2">
				<button class="btn btn-default icon-btn" v-on:click="changeadd"
				 @click="handleAdd()">
					<i class="fas fa-plus icon-color"></i>
				</button>
        <span class="p-1"></span>
				<button class="btn btn-default icon-btn" v-on:click="changedelete"
				 @click="handleSubtract()">
					<i class="fas fa-minus icon-color"></i>
				</button>
        <span class="p-1"></span>

				<button class="btn btn-default icon-btn" v-on:click="changeHidden" 
				 @click="handleEdit()">
					<i class="fas fa-edit icon-color" ></i>
				</button>
            </div>
        <div class="col-sm-10 ">
            <button type="button" class="btn btn-danger right" @click="ResetEvent()">Cancel</button>
            <!-- <span class="p-1"></span> -->
            <button type="button" class="btn btn-success right"  @click="submitEvent()">Save</button>
        </div>
  </div>
  <div class="row">
                <div class="offset-sm-3 col-sm-6">
                    <table id="listdetails">
                            <tr class="checklist-row">
                                <th v-if="islistSubtract"></th>
                                <th>List</th>
                            </tr>
                            <tr v-for="value in List" v-if="!islistedit">
                                <td v-if="islistSubtract">
					<i class="fas fa-minus icon-color" v-on:click="changesubtract(value.value)"></i>
                                   </td>   
                                <td >{{ value.list}}</td>
                            </tr>
                            <tr v-if="islistAdd">
                                    <div class="form-group">
                                    <input type="text" @change="onTextFieldchange()" v-model="value" class="form-control" placeholder="Enter your Name" >
                                    </div>
                            </tr>
                            <tr v-for="value in List" v-if="islistedit">
                                    <div class="form-group">
                                    <input type="text" @change="onEditFieldchange(value.list,value.value)"  v-model="value.list" class="form-control" >
                                    </div>
                            </tr>
                        </table>
                        </div>
                </div>
  </div>
</div>
</template>

<script>
const List=[
    {value:0,list:'Name'},
    {value:1,list:'Name1'},
    {value:2,list:'Name2'},
    {value:3,list:'Name3'},
    {value:4,list:'Name4'},
    {value:5,list:'Name5'},
    {value:6,list:'Name6'},
    {value:7,list:'Name7'},
    {value:8,list:'Name8'},
    {value:9,list:'Name9'},
    {value:10,list:'Name10'},
    {value:11,list:'Name11'},
    {value:12,list:'Name12'},
    {value:13,list:'Name13'},
    {value:14,list:'Name14'},
    {value:15,list:'Name15'},
    {value:16,list:'Name16'},
    {value:17,list:'Name17'},
    {value:18,list:'Name18'},
    {value:19,list:'Name19'},
    {value:20,list:'Name20'}              
];
export default {
       props: {
            islistAdd:Boolean,
            islistedit:Boolean,
            islistSubtract:Boolean,
            isadd:Boolean,
            isdelete:Boolean,
     },
     data: function()
    {
        return{
                List,
        }
    },
    methods: {           
            handleAdd()
            {
                this.ResetEvent();
                this.islistAdd=true;
            },
            changeadd()
            {
                this.isadd=true;
            },
            handleSubtract()
            {
                this.ResetEvent();  
                this.islistSubtract=true;
            },
            changedelete()
            {
                this.isdelete=true;
            },
            handleEdit()
            {
                this.ResetEvent();
                this.islistedit=true;
            },
            changeHidden()
            {       
                this.isHidden=true;
            },
            submitEvent()
            {
                let value=this.List.length;
                var list=this.listValue;
                if (list!="")
                {List.push({value,list});}
                this.listValue='';
                this.islistAdd=false;
                this.islistedit=false;
                this.islistSubtract=false;
            },
            ResetEvent()
            {
                this.islistSubtract=false;
                this.islistAdd=false;
                this.islistedit=false;
            },
            changesubtract(value)
            {
                List.splice(value,1);
            },
            onTextFieldchange()
            {
                this.listValue=this.value;
                this.value='';
            },
           onEditFieldchange(value,data)
            {
                var list=value;
                var value1=data;
                List.push({value1,list});
                List.pop();
            },
    } 
}
</script>

<style scoped>
.icon-btn
{
    background-color:#ffffff;
    border:1px solid #3c3c3c !important;
    padding: 0.1875rem 0.5rem;
}
.btn:focus, .btn.focus 
{
    box-shadow: none;
}
.right
{
    float:right;
}
#listdetails
{
    width:100%;
    color:#000000;
}

table > tr > th 
{
    background-color: #ebebeb;
    color: #000000;
}

.text-color-popup
{
    color:#3c3c3c;
}
th, td 
{
    padding: 5px;
    text-align: left;    
}
table > tr:hover
{
    background-color:#3e87ed;
}
.form-group{
    display: block;
    margin : 2px auto;
}

table tr:nth-child(even) {background-color: #fafafa;}
table tr:nth-child(odd) {background-color:#fbfbfb;}
</style>
