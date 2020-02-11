<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>NameGator</h1>
      <h6>Informe possíveis prefixos e sufixos para receber possibilidades de nome</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos
              <span class="badge badge-info">{{prefixes.length}}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">
                        {{prefix}}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="removePrefix(prefix)"><span class="fa fa-trash"></span></button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    v-model="prefix"
                    v-on:keyup.enter="addPrefix(prefix)"
                    placeholder="Adicione mais um prefixo"
                  />
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>
              Sufixos
              <span class="badge badge-info">{{sufixes.length}}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{sufix}}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="removeSufix(sufix)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input
                    class="form-control"
                    type="text"
                    v-model="sufix"
                    v-on:keyup.enter="addSufix(sufix)"
                    placeholder="Adicione mais um sufixo"
                  />
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
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
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: "App",
	data: () => ({
		prefix: "",
		sufix: "",
		prefixes: ["Air", "Jet"],
		sufixes: ["hub", "mart"],
	}),
	methods: {
		addPrefix(prefix) {
			if (!this.prefixes.some(val => val == prefix)) {
				this.prefixes.push(prefix);
				this.prefix = "";

			} else {
				this.prefix = "";
			}
		},
		addSufix(sufix) {
			if (!this.sufixes.some(val => val == sufix)) {
				this.sufixes.push(sufix);
				this.sufix = "";
			} else {
				this.sufix = "";
			}
		},
		removePrefix(prefix){
			this.prefixes.splice(this.prefixes.indexOf(prefix),1);
		},
		removeSufix(sufix){
			this.sufixes.splice(this.sufixes.indexOf(sufix),1);
		},
		
	},
	computed:{
		domains() {
			const domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					const name = prefix + sufix;
					const url = name.toLowerCase();
					domains.push({name:name,link:`https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com&_ga=2.267258118.908109154.1581444100-743799972.1581444100`});
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
