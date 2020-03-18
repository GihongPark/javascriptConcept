# DocumentFragment
DOM 객체는 노드가 추가 / 삭제 등 변경이 일어날때 마다 DOM Tree에 접근해 노드의 위치를 다시 계산하는 reflow가 일어나기 때문에 성능 저하가 있습니다.
따라서 막대한 크기의 DOM 객체에 다수의 요청이 일어날 경우를 대비해 `DocumentFragment`를 사용할 수 있습니다.

`DocumentFragment`는 **메모리상**에 노드 구조를 생성 및 연산 후 활성화 된 DOM 구조에 삽입함으로써 reflow를 일으키지 않습니다.

## DocumentFragment 생성
### appendChild, insertBefore
`document.createDocumentFragment()`를 사용하여 `DocumentFragment`를 생성하고 `appendChild()`나 `insertBefore()`를 통해 DOM에 추가할 수 있습니다.
```javascript
const fragment = document.createDocumentFragment();

['apple', 'banana', 'orange', 'strawberry'].forEach(e => {
    const li = document.createElement('li');
    li.textContent = e;

    fragment.appendChild(li);
});
document.body.appendChild(fragment);
```

### innerHTML
위의 방법을 사용할 경우 노드가 많아질수록 매우 번거롭기 때문에 아래 방법과 같이 `innerHTML`를 사용하여 좀 더 간편하게 생성할 수 있습니다.
```javascript
const fragment = document.createDocumentFragment();

const div = document.createElement('div');
div.innerHTML = `
    <li>apple</li>
    <li>banana</li>
    <li>orange</li>
    <li>strawberry</li>
`;
fragment.appendChild(div);

document.body.appendChild(fragment);
```