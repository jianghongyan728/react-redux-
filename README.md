## react-redux的结合使用
##### 首先我们先用react创建文件

```
npm install -g create-react-app//安装全局
create-react-app react-redux//创建文件

cd react-redux//跳转文件
npm start//运行
```
##### 我们把文件创建完之后，还要安装react-redux

```
npm install react-redux --save
如果安装的慢或者安装出错误，就可以用cnpm
npm install cnpm -g//安装全局的cnpm
cnpm install react-redux --save//安装完cnpm，在安装react-redux
```
##### 接下来就看看我们的代码吧
###### App.js

```javascript
import React, { Component } from 'react';
import Calc from './component/Calc';
import CalcContainer from './container/CalcContainer';

class App extends Component {
  constructor(props){
      super();
  }
  render() {
    return (
        
          <CalcContainer>
            <Calc />
          </CalcContainer>
    );
  }
}

export default App;

```

###### Calc.js

```javascript
import React from 'react';

const Calc = (props) => {
    let{number,onPlus,onMinus,onOdd,onAnync}=props;
    return (
        <div>
           <span id="spanResult">{number}</span>
            <br/>
            <input id="btn1" type="button" value="plus" onClick={onPlus}/>
            <input id="btn2" type="button" value="minus" onClick={onMinus}/>
            <input id="btn3" type="button" value="if odd plus" onClick={onOdd}/>
            <input id="btn4" type="button" value="anync plus" onClick={onAnync}/> 
        </div>
    );
};

export default Calc;
```
###### index.js

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import {createStore} from 'redux';
import reducer from './reducer/index';
import {Provider} from 'react-redux';

let store =createStore(reducer);

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>
, document.getElementById('root'));
registerServiceWorker();

```
###### CalcContainer.js

```javascript
import React from 'react';
import Calc from '../component/Calc';
import {connect} from 'react-redux';

const mapStoreToProps=(state,ownProps)=>{
    return{
        number:state
    }
}

const mapDispatchToProps=((dispatch,ownProps)=>{
   return{
        onPlus:()=>{
        dispatch({
        type:"plus"
        })
    },
        onMinus:()=>{
        dispatch({
            type:"jian"
            })
    },
        onOdd:()=>{
        dispatch({
            type:"odd_plus"
            })
    },
        onAnync:()=>{
        setTimeout(function(){
            dispatch({
                type:"async_plus"
            })
            },1000)
         }
    }
})

let CalcContainer=connect(mapStoreToProps,mapDispatchToProps)(Calc);

export default CalcContainer;
```
##### 以上就是所有的代码，接下来我们看看效果，当点击plus的时候+1，点击minus就-1，点击if odd plus奇数的时候+1，点击anync plus异步1秒后+1


![看这里](https://github.com/jianghongyan728/react-redux-/blob/master/GIF.gif);


