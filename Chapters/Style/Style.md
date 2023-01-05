## Styling Applications
    .lightGreen [ Draw { #color: #B3E6B5 } ],
    .lightBlue [ Draw { #color: #lightBlue } ] ]'
    .lightGreen [ Draw { #color: #B3E6B5 } ],
    .lightBlue [ Draw { #color: #lightBlue } ] ]'
    .codeFont [ Font { #name: EnvironmentFont(#code) } ],
    .textFont [ Font { #name: EnvironmentFont(#default) } ]
]'
	Font { #bold: true }
]'
presenter application: (app := SpApplication new).

styleSheet := SpStyle defaultStyleSheet, 
	(SpStyleVariableSTONReader fromString: 
	'.application [
	     Font { #bold: true },
            .lightGreen [ Draw { #color: #B3E6B5 } ],
            .bgBlack [ Draw { #backgroundColor: #black } ],
	    .blue [ Draw { #color: #blue } ]
]' ).

app styleSheet: styleSheet.
	add: (label := presenter newLabel);
	yourself).

label label: 'I am a label'.
label addStyle: 'lightGreen'.
label addStyle: 'black'.

presenter openWithSpec.
label removeStyle: 'bgBlack'.
label addStyle: 'blue'.
	slots: {};
	package: 'Spec-workshop'

	^ SpStyle defaultStyleSheet, 
		(SpStyleVariableSTONReader fromString:
	'.application [
		Font { #bold: true },
		.lightGreen [ Draw { #color: #B3E6B5 } ],
		.lightBlue [ Draw { #color: #lightBlue } ],
		.container [ Container { #padding: 4, #borderWidth: 2 } ],
		.bgOpaque [ Draw { #backgroundColor: EnvironmentColor(#base) } ],
		.codeFont [ Font { #name: EnvironmentFont(#code) } ],
		.textFont [ Font { #name: EnvironmentFont(#default) } ],
		.bigFontSize [ Font { #size: 20 } ],
		.smallFontSize [ Font { #size: 14 } ],
		.icon [ Geometry { #width: 30 } ],
		.buttonStyle [ Geometry { #width: 110 } ],
		.labelStyle [ 
			Geometry { #height: 25 },
			Font { #size: 12 }	]
	]')
	slots: { #text . #label . #zoomOutButton . #textFontButton . #codeFontButton . #zoomInButton };
	package: 'Spec-workshop'

	self instantiatePresenters.
	self initializeStyles.
	self initializeLayout

	zoomInButton := self newButton.
	zoomInButton icon: (self iconNamed: #glamorousZoomIn).
	zoomOutButton := self newButton.
	zoomOutButton icon: (self iconNamed: #glamorousZoomOut).

	codeFontButton := self newButton.
	codeFontButton
		icon: (self iconNamed: #smallObjects);
		label: 'Code font'.
	textFontButton := self newButton.
	textFontButton
		icon: (self iconNamed: #smallFonts);
		label: 'Text font'.

	text := self newText.
	text
		beNotEditable
		clearSelection;
		text: String loremIpsum.

	label := self newLabel.
	label label: 'Lorem ipsum'
	
	self layout: (SpBoxLayout newTopToBottom
		add: label expand: false;
		add: (SpBoxLayout newLeftToRight
			add: textFontButton expand: false;
			add: codeFontButton expand: false;
			addLast: zoomOutButton expand: false;		
			addLast: zoomInButton expand: false;
			yourself)
		expand: false;
		add: text;
		yourself)

	aWindowPresenter
		title: 'Using styles';
		initialExtent: 600 @ 400

    "Change the height and size of the label and the color as ligthgreen"
    label addStyle: 'labelStyle'.
    label addStyle: 'lightGreen'.

    "The default font of the text will be the code font and 
	the font size will be the small one."
    text addStyle: 'codeFont'.
    text addStyle: 'smallFontSize'.
	
    "Change the background color."
    text addStyle: 'bgOpaque'.

    "But a smaller width for the zoom buttons"
    zoomInButton addStyle: 'icon'.
    zoomOutButton addStyle: 'icon'.
	
    codeFontButton addStyle: 'buttonStyle'.
    textFontButton addStyle: 'buttonStyle'.

    "As this presenter is the container, set to self the container
    style to add a padding and border width."
	
    self addStyle: 'container'

	(self new: CustomStylesPresenter) openWithSpec

	zoomInButton action: [
		text removeStyle: 'smallFontSize'.
		text addStyle: 'bigFontSize' ].
	zoomOutButton action: [ 
		text removeStyle: 'bigFontSize'.
		text addStyle: 'smallFontSize'].

	codeFontButton action: [
		text removeStyle: 'textFont'.
		text addStyle: 'codeFont' ].
	textFontButton action: [ 
		text removeStyle: 'codeFont'.
		text addStyle: 'textFont']