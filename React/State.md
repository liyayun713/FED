# React State(状态)
```jsx
<body>
  <div id="example"></div>
  <script type="text/babel">
    var StateComponent = React.createClass({
      getInitialState: function () {
        return {
          liked: false
        };
      },
      toggleLike: function () {
        this.setState({
          this.like: !this.state.like
        })
      },
      render: function () {
        var text = this.state.liked ? '喜欢' : '不喜欢';
        return {
          <p onClick={this.toggleLike}>我是{text}，点击改变</p>
        }
      }
    })
    
    ReactDOM.render(
      <StateComponent />,
      document.getElementById('example')
    )
  </script>
</body>
```
