---
date: 2024-08-14
---
# 주제: [[Flutter]]
재사용할 수 있는 Widget 제작
```dart
class Button Extends StatelessWidget {
	final String inputText;
	final Color backgroundColor;
	Color? textColor = Colors.black;

	Button({
		super.key,
		required this.inputText,
		required this.backgroundColor,
		this.textColor,
	});

	@override
	Widget build(BuildContext context) {
		return Container(
			decoration: BoxDecoration(
				color: backgroundColor,
				borderRadius: BorderRadius.circular(45),
			),
			child: Padding(
				padding: EdgeInsets.symmetric(
					vertical: 20,
					horizontal: 50,
				),
				child: Text(
					inputText,
					style: TextStyle(
						color: textColor,
						fontSize: 20,
					),
				),
			),
		);
	}
}
```