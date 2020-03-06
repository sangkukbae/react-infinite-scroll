# react-infinite-scroll

## [onscroll event](https://www.w3schools.com/jsref/event_onscroll.asp)
```jsx
componentDidMount() {
    // Detect when scrolled to bottom.
    this.refs.myscroll.addEventListener("scroll", () => {
      if (
        this.refs.myscroll.scrollTop + this.refs.myscroll.clientHeight >=
        this.refs.myscroll.scrollHeight
      ) {
        this.loadMore();
      }
    });
  }
```

```jsx
loadMore() {
    this.setState({ loading: true });
    setTimeout(() => {
      this.setState({ items: this.state.items + 20, loading: false });
    }, 2000);
  }
```

[https://codesandbox.io/s/react-infinite-scroll-518zt](https://codesandbox.io/s/react-infinite-scroll-518zt)



## [IntersectionObserver](https://developer.mozilla.org/ko/docs/Web/API/IntersectionObserver)
```jsx
componentDidMount() {
    this.getPhotos(this.state.page);

    var options = {
      root: null,
      rootMargin: "0px",
      threshold: 1.0
    };

    this.observer = new IntersectionObserver(
      this.handleObserver.bind(this),
      options
    );
    this.observer.observe(this.loadingRef);
  }
```

```jsx
handleObserver(entities, observer) {
    const y = entities[0].boundingClientRect.y;
    if (this.state.prevY > y) {
      const lastPhoto = this.state.photos[this.state.photos.length - 1];
      const curPage = lastPhoto.albumId;
      this.getPhotos(curPage);
      this.setState({ page: curPage });
    }
    this.setState({ prevY: y });
  }
```

[https://codesandbox.io/s/react-infinite-scroll-intersectionobserver-pk1dh](https://codesandbox.io/s/react-infinite-scroll-intersectionobserver-pk1dh)

## [react-infinite-scroller](https://www.npmjs.com/package/react-infinite-scroller)
 ```jsx
 render() {
    return (
      <div className="App">
        <header className="App-header">
          <h1>react-infinite-scroller</h1>
        </header>
        <div style={{ height: "200px", overflow: "auto" }}>
          <InfiniteScroll
            loadMore={this.loadMore.bind(this)}
            hasMore={this.state.hasMoreItems}
            loader={<div className="loader"> Loading... </div>}
            useWindow={false}
          >
            {this.showItems()}{" "}
          </InfiniteScroll>{" "}
        </div>{" "}
      </div>
    );
  }
  ```
  [https://codesandbox.io/s/react-infinite-scroller-6kh1v](https://codesandbox.io/s/react-infinite-scroller-6kh1v)

**참고 자료**
* [https://css-tricks.com/the-difference-between-throttling-and-debouncing/](https://css-tricks.com/the-difference-between-throttling-and-debouncing/)
* [https://css-tricks.com/debouncing-throttling-explained-examples/](https://css-tricks.com/debouncing-throttling-explained-examples/)
* [https://sung.codes/blog/2018/08/11/infinite-scrolling-in-react-using-javascript-generator/](https://sung.codes/blog/2018/08/11/infinite-scrolling-in-react-using-javascript-generator/)
* [https://www.npmjs.com/package/react-intersection-observer](https://www.npmjs.com/package/react-intersection-observer)
* [https://www.npmjs.com/package/react-window-infinite-loader](https://www.npmjs.com/package/react-window-infinite-loader)
* [https://stackoverflow.com/questions/21064101/understanding-offsetwidth-clientwidth-scrollwidth-and-height-respectively/33672058](https://stackoverflow.com/questions/21064101/understanding-offsetwidth-clientwidth-scrollwidth-and-height-respectively/33672058)

![alt text](https://i.stack.imgur.com/5AAyW.png "css box model")
