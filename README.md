# react-native-db
Forked from https://github.com/thewei/react-native-store

This module was inspired by Laravel's excellent Eloquent API. But I've not had enough time yet to reach anywhere near feature parity or even change from using static methods for most. Pull requests are welcome!

## Setup

### Install

`yarn add gjrdiesel/react-native-db@latest`

### Setup models

Create your own DB file once and add all your models there:
```js
import {Store} from 'react-native-db'

export default DB = {
  'users': Store.model('users'),
  'posts': Store.model('posts')
}
```

Create model classes (ex: User.js)
```js
import {Model} from 'react-native-db'

export default class User extends Model {

    static _table = 'users'
    // don't forget to add to db.js

    constructor(data)
    {
        super({
            data,
            defaults: {
                created_at: null // automatically creates a created_at timestamp when possible
            }
        })
    }

}
```

## Usage

```js
import React, { Component } from 'react';
import { Text } from 'react-native';

import User from './User'

export class Cash extends Component {
    componentWillMount(){
        User.all({ where: { registered: true }}).then(users=>this.setState({users}))
    }
    
    render(){
        return <Text>{this.state.users.length} Registered Users</Text>
    }
}
```

## All methods

- *static* `Model.create(data)` __returns promise with new Model__
- `Model.save()` __returns promise with updates *Note: this will update or save a model depending if it has an _id or not__
- *static* `Model.update(model,data,where?)` __returns promise with updated Model *Note: if you don't specify a where, it'll use _id__
- *static* `Model.updateOrCreate(model,data,where?)` __returns promise with either an updated or newly created model *Note: if you don't specify a where, it'll use _id__
- *static* `Model.delete(model)` __returns promise true__
- *static* `Model.findById(id)`
- *static* `Model.deleteAll(filter)`
- *static* `Model.all(filter)`
