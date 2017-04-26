# MapKitAutocomplete

A simple example showing Apple MapKit's autocomplete functionality.


<a href="https://imgflip.com/gif/1nx9ek"><img src="https://i.imgflip.com/1nx9ek.gif" title="made at imgflip.com"/></a>


### Highlighting search query

The method below allows you to highlight the user's search string within the tableView.

```swift
/**
  Highlights the matching search strings with the results
  - parameter text: The text to highlight
  - parameter ranges: The ranges where the text should be highlighted
  - parameter size: The size the text should be set at 
  - returns: A highlighted attributed with the ranges highlighted
 */
func highlightedText(_ text: String, inRanges ranges: [NSValue], size: CGFloat) -> NSAttributedString {
    let attributedText = NSMutableAttributedString(string: text)
    let regular = UIFont.systemFont(ofSize: size)
    attributedText.addAttribute(NSFontAttributeName, value:regular, range:NSMakeRange(0, text.characters.count))

    let bold = UIFont.boldSystemFont(ofSize: size)
    for value in ranges {
        attributedText.addAttribute(NSFontAttributeName, value:bold, range:value.rangeValue)
    }
    return attributedText
}
```

All you need to do is slightly modify the ```cellForRowAtIndexPath``` method inside your ```UITableViewDataSource``` to use attributed strings as follows:

```swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let searchResult = searchResults[indexPath.row]
    let cell = UITableViewCell(style: .subtitle, reuseIdentifier: nil)

    cell.textLabel?.attributedText = highlightedText(searchResult.title, inRanges: searchResult.titleHighlightRanges, size: 17.0)
    cell.detailTextLabel?.attributedText = highlightedText(searchResult.subtitle, inRanges: searchResult.subtitleHighlightRanges, size: 12.0)

    return cell
}
```

You can see here that we replaced the standard title and subtitle with attributed strings to embolden the text that matches the search query.

<a href="https://imgflip.com/gif/1nxa3h"><img src="https://i.imgflip.com/1nxa3h.gif" title="made at imgflip.com"/></a>
