# Двоичное(бинарное) дерево: обход

<br> Мы можем спускаться по дереву, в каждом из узлов есть выбор куда можем пойти в первую очередь и какой из элементов обработать сначала: левое поддерево, корень или право поддерево. Такие варианты обхода называются обходы в глубину (depth first).<br/>

<br>Какие возможны варианты обхода (слово поддерево опустим):<br/>

- корень, левое, правое (preorder, прямой);
- корень, правое, левое;
- левое, корень, правое (inorder, симметричный, центрированный);
- левое, правое, корень (postorder, обратный);
- правое, корень, левое;
- правое, левое, корень.

<br>Также используется вариант для обхода деревьев по уровням. Уровень в дереве — его удалённость от корня. Сначала обходится корень, после этого узлы первого уровня и так далее. Называется обход в ширину, по уровням, breadth first, BFS — breadth first search или level order traversal.<br/>

<br>Выбирается один из этих вариантов, и делается обход, в каждом из узлов применяя выбранную стратегию.<br/>

> Обычно для обходов в глубину применяется рекурсия. Реализуем один из вариантов, например симметричный: левое поддерево, корень, правое поддерево.

<br>При этом мы обработаем первым самый левый узел, где левое поддерево окажется пустым, но правое может присутствовать. То есть в каждом из узлов будем спускаться ниже и ниже, пока левое поддерево не окажется пустым.<br/>

```
class BinaryTreeItem {
  constructor(itemValue) {
    this.value = itemValue;
    this.left = null;
    this.right = null;
  }
}

const elementExistMessage =
  "The element has already in the tree";

class BinaryTree {
  constructor() {
    this.root = null;
  }

  insertItem(newItem) {
    // .....
  }

  breadthFirstHandler(handlerFunction) {
    if (this.root === null) return;

    // массив, в который будем добавлять элементы,
    // по мере спускания по дереву
    const queue = [this.root];
    // используем позицию в массиве для текущего
    // обрабатываемого элемента
    let queuePosition = 0;

    // можем убирать обработанные элементы из очереди
    // например функцией shift
    // для обработки всегда брать нулевой элемент
    // и завершать работу, когда массив пуст
    // но shift работает за линейное время, что увеличивает
    // скорость работы алгоритма
    // while (queue.length > 0) {
    //   const currentNode = queue.shift();

    while (queuePosition < queue.length) {
      // текущий обрабатываемый элемент в queuePosition
      const currentNode = queue[queuePosition];
      handlerFunction(currentNode.value);

      // добавляем в список для обработки дочерние узлы
      if (currentNode.left !== null) {
        queue.push(currentNode.left);
      }
      if (currentNode.right !== null) {
        queue.push(currentNode.right);
      }

      queuePosition++;
    }
  }

  _insertItem(currentNode, newNode) {
    // ......
  }
}

const binaryTree = new BinaryTree();
binaryTree.insertItem(3);
binaryTree.insertItem(1);
binaryTree.insertItem(6);
binaryTree.insertItem(4);
binaryTree.insertItem(8);
binaryTree.insertItem(-1);
binaryTree.insertItem(3.5);

binaryTree.breadthFirstHandler(console.log);
// вызов breadthFirstHandler(console.log) выведет
// 3 корень
// 1 узлы первого уровня
// 6
// -1 узлы второго уровня
// 4
// 8
// 3.5 узел третьего уровня
```
