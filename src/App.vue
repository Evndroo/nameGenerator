<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Name generator</h1>
      <h6>Informe possíveis prefixos e sufixos para receber possibilidades de nome</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <ItemList title="Prefixos" v-bind:items="prefixes" v-on:addItem="addPrefix" v-on:removeItem="removePrefix"></ItemList>
          </div>
          <div class="col-md">
            <ItemList title="Sufixos" v-bind:items="sufixes" v-on:addItem="addSufix" v-on:removeItem="removeSufix"></ItemList>
          </div>
        </div>

        <div id="domains" class="container">
          <h5>
            Domínios
            <span class="badge badge-info">{{domains.length}}</span>
          </h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">
                  <div class="row">
                    <div class="col-md">{{domain.name}}</div>
                    <div class="col-md text-right">
                      <a class="btn btn-info" target="blank" v-bind:href="domain.link">
                        <span class="fa fa-shopping-cart"></span>
                      </a>
                    </div>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import ItemList from "./Components/ItemList";

export default {
	name: "App",
	components: {
		ItemList
	},
	data: () => ({
		prefix: "",
		sufix: "",
		prefixes: ["Air", "Jet"],
		sufixes: ["hub", "mart"]
	}),
	methods: {
		addPrefix(prefix) {
			if (!this.prefixes.some(val => val == prefix)) {
				this.prefixes.push(prefix);
			} 
		},
		addSufix(sufix) {
			if (!this.sufixes.some(val => val == sufix)) {
				this.sufixes.push(sufix);
			}
		},
		removePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
		},
		removeSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
		}
	},
	computed: {
		domains() {
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					const name = prefix + sufix;
					const url = name.toLowerCase();
					domains.push({
						name: name,
						link: `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com&_ga=2.267258118.908109154.1581444100-743799972.1581444100`
					});
				}
			}
			console.log(domains);
			return domains;
		}
	}
};
</script>

<style>
h6 {
  margin-top: 15px;
}

#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}

#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}

#domains {
  margin-top: 30px;
}
</style>
