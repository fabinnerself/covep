<template>
  <div>
    <h2>Operaciones con Producto</h2>
    <LinkButton iconCls="icon-add" @click="addRow()" style="width:80px;margin-bottom:4px">Adicionar</LinkButton>
    <LinkButton iconCls="icon-edit" @click="editRow()" style="width:80px;margin-bottom:4px">Editar</LinkButton>
    <LinkButton iconCls="icon-delete" @click="deleteRow()" style="width:80px;margin-bottom:4px">Eliminar</LinkButton>
    <LinkButton iconCls="icon-search" @click="fn_buscar()" style="width:80px;margin-bottom:4px">Buscar</LinkButton>
    <LinkButton iconCls="icon-undo" @click="fn_limpiar()" style="width:80px;margin-bottom:4px">Limpiar</LinkButton>
    <LinkButton iconCls="icon-home" @click="fn_principal()" style="width:80px;margin-bottom:4px">Principal</LinkButton>

    <DataGrid ref="datagrid"
              :data="data" style="height:450px; width:850px"
              :columnResizing="true"
              :filterable="filterable"
              :pagination="true"
              :selectionMode="selectionMode"
              @selectionChange="selection=$event">
      <GridColumn align="center" cellCss="datagrid-td-rownumber" width="30">
        <template v-slot:body="scope">
          {{ scope.rowIndex + 1 }}
        </template>
      </GridColumn>
      <GridColumn field="id" title="ID" filterable></GridColumn>
      <GridColumn field="name" title="Nombre" filterable></GridColumn>
      <GridColumn field="description" title="Descripcion" filterable></GridColumn>
      <GridColumn field="price" title="Precio" align="right" filterable>
        <template v-slot:body="scope">
          {{ formatPrice(scope.row.price) }}
        </template>
      </GridColumn>
    </DataGrid>

    <Dialog ref="dlg" bodyCls="f-column" :title="title" :modal="true" closed :dialogStyle="{height:'311px'}">
      <div class="f-full" style="overflow:auto">
        <Form ref="form" :model="model" :rules="rules" @validate="errors=$event" style="padding:5px 25px">
          <div style="margin-bottom:20px">
            <Label for="id">ID:</Label>
            <TextBox inputId="id" name="id" v-model="model.id"></TextBox>
            <div class="error">{{ getError('id') }}</div>
          </div>
          <div style="margin-bottom:20px">
            <Label for="name">Nombre:</Label>
            <TextBox inputId="name" name="name" v-model="model.name"></TextBox>
            <div class="error">{{ getError('name') }}</div>
          </div>
          <div style="margin-bottom:20px">
            <Label for="description">Descripcion:</Label>
            <TextBox inputId="description" name="description" v-model="model.description"></TextBox>
            <div class="error">{{ getError('description') }}</div>
          </div>
          <div style="margin-bottom:20px">
            <Label for="price">Precio:</Label>
            <NumberBox inputId="price" name="price" :precision="2" v-model="model.price"></NumberBox>
          </div>
        </Form>
      </div>
      <div class="buttons f-noshrink">
        <LinkButton iconCls="icon-ok" @click="saveRow()">Grabar</LinkButton>
        <LinkButton iconCls="icon-cancel" @click="$refs.dlg.close()">Cancelar</LinkButton>
      </div>
    </Dialog>
  </div>
</template>

<script>
export default {
  name: 'ProductOperations',
  data() {
    return {
      data: [
        {
          id: "6",
          name: "Product 6",
          description: "Description for Product 6",
          price: "69.990000"
        },{
      "id":"7",
      "name":"Product 7",
      "description":"Description for Product 7",
      "price":"79.990000"
   },
   {
      "id":"8",
      "name":"Product 8",
      "description":"Description for Product 8",
      "price":"89.990000"
   },
   {
      "id":"9",
      "name":"Product 9",
      "description":"Description for Product 9",
      "price":"99.990000"
   },
   {
      "id":"10",
      "name":"Product 10",
      "description":"Description for Product 10",
      "price":"109.990000"
   },
   {
      "id":"12",
      "name":"producto aa",
      "description":"descripcion de aa",
      "price":"11.000000"
   },
   {
      "id":"13",
      "name":"mi producto",
      "description":"nuevo prod",
      "price":"80.000000"
   },
   {
      "id":"14",
      "name":"poco mas++",
      "description":"celular xiomi poco ml++",
      "price":"10000.010000"
   },
   {
      "id":"15",
      "name":"Product 1",
      "description":"Description for Product 1",
      "price":"10.000000"
   },
   {
      "id":"16",
      "name":"Product 2",
      "description":"Description for Product 2",
      "price":"20.000000"
   },
   {
      "id":"17",
      "name":"Product 3",
      "description":"Description for Product 3",
      "price":"30.000000"
   },
   {
      "id":"18",
      "name":"Product 4",
      "description":"Description for Product 4",
      "price":"40.000000"
   },
   {
      "id":"19",
      "name":"Product 5",
      "description":"Description for Product 5",
      "price":"50.000000"
   },
   {
      "id":"20",
      "name":"Product 6",
      "description":"Description for Product 6",
      "price":"60.000000"
   },
   {
      "id":"21",
      "name":"Product 7",
      "description":"Description for Product 7",
      "price":"70.000000"
   },
   {
      "id":"22",
      "name":"Product 8",
      "description":"Description for Product 8",
      "price":"80.000000"
   },
   {
      "id":"23",
      "name":"Product 9",
      "description":"Description for Product 9",
      "price":"90.000000"
   },
   {
      "id":"24",
      "name":"Product 10",
      "description":"Description for Product 10",
      "price":"100.000000"
   },
   {
      "id":"25",
      "name":"Product 11",
      "description":"Description for Product 11",
      "price":"110.000000"
   },
   {
      "id":"26",
      "name":"Product 12",
      "description":"Description for Product 12",
      "price":"120.000000"
   },
   {
      "id":"27",
      "name":"Product 13",
      "description":"Description for Product 13",
      "price":"130.000000"
   },
   {
      "id":"28",
      "name":"Product 14",
      "description":"Description for Product 14",
      "price":"140.000000"
   },
   {
      "id":"29",
      "name":"Product 15",
      "description":"Description for Product 15",
      "price":"150.000000"
   },
   {
      "id":"30",
      "name":"Product 16",
      "description":"Description for Product 16",
      "price":"160.000000"
   },
   {
      "id":"31",
      "name":"Product 17",
      "description":"Description for Product 17",
      "price":"170.000000"
   },
   {
      "id":"32",
      "name":"Product 18",
      "description":"Description for Product 18",
      "price":"180.000000"
   },
   {
      "id":"33",
      "name":"Product 19",
      "description":"Description for Product 19",
      "price":"190.000000"
   },
   {
      "id":"34",
      "name":"Product 20",
      "description":"Description for Product 20",
      "price":"200.000000"
   },
   {
      "id":"35",
      "name":"Product 21",
      "description":"Description for Product 21",
      "price":"210.000000"
   },
   {
      "id":"36",
      "name":"Product 22",
      "description":"Description for Product 22",
      "price":"220.000000"
   },
   {
      "id":"37",
      "name":"Product 23",
      "description":"Description for Product 23",
      "price":"230.000000"
   },
   {
      "id":"38",
      "name":"Product 24",
      "description":"Description for Product 24",
      "price":"240.000000"
   },
   {
      "id":"39",
      "name":"Product 25",
      "description":"Description for Product 25",
      "price":"250.000000"
   },
   {
      "id":"40",
      "name":"Product 26",
      "description":"Description for Product 26",
      "price":"260.000000"
   },
   {
      "id":"41",
      "name":"Product 27",
      "description":"Description for Product 27",
      "price":"270.000000"
   },
   {
      "id":"42",
      "name":"Product 28",
      "description":"Description for Product 28",
      "price":"280.000000"
   },
   {
      "id":"43",
      "name":"Product 29",
      "description":"Description for Product 29",
      "price":"290.000000"
   },
   {
      "id":"44",
      "name":"Product 30",
      "description":"Description for Product 30",
      "price":"300.000000"
   },
   {
      "id":"45",
      "name":"Product 31",
      "description":"Description for Product 31",
      "price":"310.000000"
   },
   {
      "id":"46",
      "name":"Product 32",
      "description":"Description for Product 32",
      "price":"320.000000"
   },
   {
      "id":"47",
      "name":"Product 33",
      "description":"Description for Product 33",
      "price":"330.000000"
   },
   {
      "id":"48",
      "name":"Product 34",
      "description":"Description for Product 34",
      "price":"340.000000"
   },
   {
      "id":"49",
      "name":"Product 35",
      "description":"Description for Product 35",
      "price":"350.000000"
   },
   {
      "id":"50",
      "name":"Product 36",
      "description":"Description for Product 36",
      "price":"360.000000"
   },
   {
      "id":"51",
      "name":"Product 37",
      "description":"Description for Product 37",
      "price":"370.000000"
   },
   {
      "id":"52",
      "name":"Product 38",
      "description":"Description for Product 38",
      "price":"380.000000"
   },
   {
      "id":"53",
      "name":"Product 39",
      "description":"Description for Product 39",
      "price":"390.000000"
   },
   {
      "id":"54",
      "name":"Product 40",
      "description":"Description for Product 40",
      "price":"400.000000"
   },
   {
      "id":"55",
      "name":"Product 41",
      "description":"Description for Product 41",
      "price":"410.000000"
   },
   {
      "id":"56",
      "name":"Product 42",
      "description":"Description for Product 42",
      "price":"420.000000"
   },
   {
      "id":"57",
      "name":"Product 43",
      "description":"Description for Product 43",
      "price":"430.000000"
   },
   {
      "id":"58",
      "name":"Product 44",
      "description":"Description for Product 44",
      "price":"440.000000"
   },
   {
      "id":"59",
      "name":"Product cuarenta y cinco",
      "description":"Description for Product xxxxv",
      "price":"451.000000"
   },
   {
      "id":"60",
      "name":"Product 46",
      "description":"Description for Product 46",
      "price":"460.000000"
   },
   {
      "id":"61",
      "name":"Product 47",
      "description":"Description for Product 47",
      "price":"470.000000"
   },
   {
      "id":"65",
      "name":"produ",
      "description":"descri",
      "price":"40.000000"
   },
   {
      "id":"66",
      "name":"poco mas",
      "description":"celular xiomi poco ml",
      "price":"101.000000"
   },
   {
      "id":"67",
      "name":"Product 004",
      "description":"Description for Product 04",
      "price":"49.990000"
   }  
      ],
      title: '',
      model: {
        id: null,
        name: null,
        description: null,
        price: null
      },
      rules: {
        name: 'required',
        description: 'required',
      },
      errors: {},
      editingRow: null,
      selectionOptions: [
        { value: null, text: "None" },
        { value: "single", text: "Single Selection" },
        { value: "multiple", text: "Multiple Selection" },
        { value: "cell", text: "Cell Selection" },
        { value: "multicell", text: "Multiple Cells" }
      ],
      selectionMode: "single",
      selection: null,
      filterable: true
    };
  },
  mounted() {
    document.title = "Productos";
  },
  methods: {
    formatPrice(value) {
      return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
    },
    addRow() {
      this.model = {
        id: null,
        name: null,
        description: null,
        price: null
      };
      this.title = 'Adición de Producto';
      this.$refs.dlg.open();
    },
    editRow() {
      if (this.selection) {
        this.editingRow = this.selection;
        this.model = { ...this.selection };
        this.title = 'Modificar Producto';
        this.$refs.dlg.open();
      } else {
        this.$messager.alert({
          title: "Advertencia",
          icon: "warning",
          msg: "Elija una fila para poder modificar"
        });
      }
    },
    saveRow() {
      this.$refs.form.validate(errors => {
        if (!errors) {
          const newRow = { ...this.model };

          if (this.editingRow) {
            const index = this.data.indexOf(this.editingRow);

            if (index !== -1) {
              this.data[index] = { ...newRow };
            }
            this.editingRow = null;
          } else {
            newRow.id = (this.data.length + 1).toString();
            this.data.unshift(newRow);
          }
          this.data = [...this.data];
          this.$refs.dlg.close();
        }
      });
    },
    deleteRow() {
       
      if (this.selection) {
        this.$messager.confirm({
          title: 'Confirmar',
          msg: '¿Está seguro de eliminar el registro de este producto?',
          result: (r) => {
            if (r) {
              const index = this.data.indexOf(this.selection);
              this.data.splice(index, 1);
              this.data = [...this.data];
            }
          }
        });
      } else {
        this.$messager.alert({
          title: "Advertencia",
          icon: "warning",
          msg: "Elija una fila para poder eliminar"
        });
      }
    },
    getError(name) {
      return this.errors[name] && this.errors[name].length
        ? this.errors[name][0]
        : null;
    },
    hasError(name) {
      return this.errors[name] && this.errors[name].length;
    },
    fn_buscar() {
      this.filterable = !this.filterable;
    },
    fn_limpiar() {
      alert("no implementado");
    },
    fn_principal() {
      window.location.href = "https://www.google.com";
    }
  }
};
</script>

<style>
.icon-delete {
  background: url('delete1.png') no-repeat center center;
}
.icon-home {
  background: url('home.png') no-repeat center center;
}
</style>
