# Keyboard-Observer

//
//  KeyboardObserver.swift
//  
//
//  Created by Jaimin Galiya on 7/2/18.
//

import Foundation

class KeyboardObserver: NSObject {
    
    ///addobserver to hide and show keyboard
    class func addObserver(view: UIScrollView, target: Any)
    {
        //scrollView = view
        NotificationCenter.default.addObserver(forName: .UIKeyboardWillShow, object: nil, queue: nil, using: {
            notification in
            keyboardWillShow(notification: notification, delegate: target, view: view)
        })
        NotificationCenter.default.addObserver(forName: .UIKeyboardWillHide, object: nil, queue: nil, using: {
            notification in
            keyboardWillHide(notification: notification, view: view)
        })
        
    }
    
    ///keyboard show in calculating scrollview contentinset
    class func keyboardWillShow(notification: Notification, delegate: Any, view: UIScrollView)
    {
        guard let userInfo = notification.userInfo,
            let frame = (userInfo[UIKeyboardFrameEndUserInfoKey] as? NSValue)?.cgRectValue else{
                return
        }
        let contentInsets = UIEdgeInsets(top: 0, left: 0, bottom: frame.height, right: 0)
        view.contentInset = contentInsets
        //        view.contentOffset = CGPoint(x: 0, y: contentInsets.bottom)
        view.scrollIndicatorInsets = contentInsets
    }
    
    ///keyboard hide
    class func keyboardWillHide(notification: Notification, view: UIScrollView)
    {
        let contentInsets = UIEdgeInsets.zero
        view.contentInset = contentInsets
        view.scrollIndicatorInsets = contentInsets
    }
    
    ///removeobserver from view
    class func removeObservers(target: Any)
    {
        NotificationCenter.default.removeObserver(target)
    }
}
