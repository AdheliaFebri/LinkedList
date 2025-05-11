  class DNode {
  int? data;
  DNode? next;
  DNode? prev;

  DNode(this.data);
}

class DoubleLinkedList {
  DNode? head;
  DNode? tail;

  bool isEmpty() => head == null;

  void insertTailNode(int data) {
    var newNode = DNode(data);
    if (isEmpty()) {
      head = tail = newNode;
    } else {
      tail!.next = newNode;
      newNode.prev = tail;
      tail = newNode;
    }
  }

  void printForward() {
    var current = head;
    print("Cetak maju:");
    while (current != null) {
      print(current.data);
      current = current.next;
    }
  }

  void printBackward() {
    var current = tail;
    print("Cetak mundur:");
    while (current != null) {
      print(current.data);
      current = current.prev;
    }
  }

  void tambahNode_SebelumBacaMundur(DNode newNode, DNode target) {
    if (isEmpty()) {
      print("List kosong. Tidak bisa menambahkan node.");
      return;
    }

    DNode? curr = tail;

    while (curr != null && curr != target) {
      curr = curr.prev;
    }

    if (curr == null) {
      print("Node target tidak ditemukan.");
      return;
    }

    if (curr == head) {
      newNode.next = head;
      head!.prev = newNode;
      head = newNode;
      return;
    }

    newNode.prev = curr.prev;
    newNode.next = curr;
    curr.prev!.next = newNode;
    curr.prev = newNode;
  }
}

void main() {
  var list = DoubleLinkedList();

  list.insertTailNode(10);
  list.insertTailNode(30);
  list.insertTailNode(50);

  print("Sebelum penambahan:");
  list.printForward();

  var newNode = DNode(20);
  var target = list.head!.next!; 
  list.tambahNode_SebelumBacaMundur(newNode, target);

  print("\nSetelah penambahan:");
  list.printForward();
}
