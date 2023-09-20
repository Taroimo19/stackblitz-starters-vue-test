<template lang="pug">
div
    h2 Search
    form.form.form-horizontal
        .form-group(:class="{ 'has-error' : errors.query }")
            label.control-label.col-xs-1 query
            .col-xs-11
                input.form-control(ref='query')
                span.help-block(v-if='errors.query') {{ errors.query }}
        .form-grup
            .col-xs-offset-1
                button.btn.btn-default(type='button', @click='search') Search
</template>

<script>
'use strict';
var Validator = require('validatorjs');
Validator.useLang('ja');

module.exports = {
    data: function(){
        return {
            errors: {
                query: ''
            }
        };
    },

    methods: {
        search: function(){
            var v = new Validator({             // validate するデータ
                query: this.$refs.query.value
            }, {                                // validate ルール
                query: 'required'
            });

            var pass = v.check();

            // エラーをセット（エラーなしの場合は、nullで上書きする）
            this.errors = {
                query: v.errors.first('query')
            };

            if(pass){
                // validate OKの場合の処理...
            }
        }
    }
}
</script>