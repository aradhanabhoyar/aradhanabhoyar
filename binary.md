pub struct BinaryTree<T> {
    root: BinaryNode<T>,
    depth: i32,
}
impl<T> BinaryTree<T> {
    pub fn new() -> Self {
        BinaryTree {
            root: BinaryNode::new(),
            depth: 0,
        }
    }
   pub fn root(&self) -> &BinaryNode<T> {
        &self.root
    }
  pub fn root_mut(&mut self) -> &mut BinaryNode<T> {
        &mut self.root
    }

    pub fn depth(&self) -> i32 {
        self.depth
    }
}

pub struct BinaryNode<T> {
    value: Option<T>,
    left: Box<Option<BinaryNode<T>>>,
    right: Box<Option<BinaryNode<T>>>,
}

impl<T> BinaryNode<T> {
    pub fn new() -> Self {
        BinaryNode {
            value: None,
            left: Box::new(None),
            right: Box::new(None),
        }
    }

    pub fn from_value(value: T) -> Self {
        BinaryNode {
            value: Some(value),
            left: Box::new(None),
            right: Box::new(None),
        }
    }

    pub fn value(&self) -> &Option<T> {
        &self.value
    }

    pub fn is_filled(&self) -> bool {
        self.value.is_some()
    }

    pub fn left(&self) -> &Option<BinaryNode<T>> {
        &(*(self.left))  
    }

    pub fn right(&self) -> &Option<BinaryNode<T>> {
        &(*(self.right)) 
    }
    pub fn append_left(&mut self, value: T) -> Result<&Option<BinaryNode<T>>, String> {
        if self.left.is_none() {
            self.left = Box::new(Some(BinaryNode::from_value(value)));
            Ok(self.left())
        } else {
            Err(String::from(
                "Can not create a new child node in left, because left is not empty.",
            ))
        }
    }
    pub fn append_right(&mut self, value: T) -> Result<&Option<BinaryNode<T>>, String> {
        if self.right.is_none() {
            self.right = Box::new(Some(BinaryNode::from_value(value)));
            Ok(self.right())
        } else {
            Err(String::from(
                "Can not create a new child node in right, because right is not empty.",
            ))
        }
    }

    pub fn clear_left(&mut self) -> Option<BinaryNode<T>> {
        let old_left = self.left.take();
        self.left = Box::new(None);
        old_left
    }

    pub fn clear_right(&mut self) -> Option<BinaryNode<T>> {
        let old_right = self.right.take();
        self.right = Box::new(None);
        old_right
    }
    pub fn set_left(&mut self, new_node: BinaryNode<T>) -> Option<BinaryNode<T>> {
        let old_left = self.left.take();
        self.left = Box::new(Some(new_node));
        old_left
    }
    pub fn set_right(&mut self, new_node: BinaryNode<T>) -> Option<BinaryNode<T>> {
        let old_right = self.right.take();
        self.right = Box::new(Some(new_node));
        old_right
    }
}

#[cfg(test)]
mod tests {

    use super::*;

    #[test]
    fn test_stuff() {
        let mut tree: BinaryTree<i32> = BinaryTree::new();
        assert!(!tree.root().is_filled());
        assert!(tree.root().left().is_none());
        assert!(tree.root().right().is_none());
        assert!(tree.root_mut().append_left(2).is_ok());
        assert!(tree.root_mut().append_right(3).is_ok());
        assert_eq!(tree.root().left().as_ref().unwrap().value().unwrap(), 2); 
        assert_eq!(tree.root().right().as_ref().unwrap().value().unwrap(), 3); 
        assert_eq!(tree.root_mut().clear_left().unwrap().value().unwrap(), 2);
        assert_eq!(tree.root_mut().clear_right().unwrap().value().unwrap(), 3);
        assert!(tree.root().left().is_none());
        assert!(tree.root().right().is_none());
        assert!(tree.root_mut().set_left(BinaryNode::from_value(4)).is_none());
        assert_eq!(tree.root().left().as_ref().unwrap().value().unwrap(), 4);
        assert!(tree.root_mut().set_right(BinaryNode::from_value(5)).is_none());
        assert_eq!(tree.root().right().as_ref().unwrap().value().unwrap(), 5);
        assert!(tree.root_mut().set_left(BinaryNode::from_value(6)).is_some_and(|node| node.value().unwrap() == 4));
        assert_eq!(tree.root().left().as_ref().unwrap().value().unwrap(), 6);
        assert!(tree.root_mut().set_right(BinaryNode::from_value(7)).is_some_and(|node| node.value().unwrap() == 5));
        assert_eq!(tree.root().right().as_ref().unwrap().value().unwrap(), 7);
    }
}
