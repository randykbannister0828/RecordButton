# RecordButton

It shows you the recording process when recording. It's great for a video recorder app with a fixed/maximum length like snapchat, vine, instragram.

![Screenshot](http://imgur.com/S69GerW.gif)

## Requirements

iOS 8 and higher

## Example Project

To run the example project, clone the repo, and run `pod install` from the Example directory first.


## Usage 

### Add a simple RecordButton

Add this to `viewDidLoad`

```swift 

let recordButton = RecordButton(frame: CGRect(x: 0,y: 0,width: 70,height: 70))
view.addSubview(recordButton) 

``` 

### Update progress 
*it's the easiest to just check out the example project for this.*

To update progress the RecordButton must be an instance of the class. You should also add a `progressTimer` and a `progress` variable, like this: 

```swift 

class ViewController: UIViewController {

	var recordButton : RecordButton!
	var progressTimer : Timer!
	var progress : CGFloat = 0
	
	// rest of viewController 
	
```

The `recordButton` needs a target for start and stopping the progress timer. Add this code after initialization of the `recordButton` (usualy in `viewDidLoad()`)

```swift

recordButton.addTarget(self, action: #selector(self.record), for: .touchDown)
recordButton.addTarget(self, action: #selector(self.stop), for: UIControl.Event.touchUpInside)

```

Finally add these functions to your ViewController 

```swift

    @objc func record() {
        self.progressTimer = Timer.scheduledTimer(timeInterval: 0.05, target: self, selector: #selector(ViewController.updateProgress), userInfo: nil, repeats: true)
    }
    
    @objc func updateProgress() {
        
        let maxDuration = CGFloat(5) // Max duration of the recordButton
        
        progress = progress + (CGFloat(0.05) / maxDuration)
        recordButton.setProgress(progress)
        
        if progress >= 1 {
            progressTimer.invalidate()
        }
        
    }
    
    @objc func stop() {
        self.progressTimer.invalidate()
    }
    
```
## Support/Issues 
If you have any questions, please don't hesitate to create an issue. 

## To Do 
* Add Carthage Support
* Add a delegation pattern
