# Simple UI language via bracket style (C, C#, Java)

Basic style:

    ViewType(attr1='value1', attr2='value2', attr3=42) {
        // Child views go here
    }
    ViewType(name='Row B') {
        ViewType(name='B, Row 1, Column 1'), ViewType(name='B, Row 1, Column 2')
        ViewType(name='B, Row 2, Column 1'), ViewType(name='B, Row 2, Column 2')
        ViewType(name='B, Row 3, Column 1'), ViewType(name='B, Row 3, Column 2')
    }
    

Ideas:
- Rows are separated by newlines. Columns are separated by commas.
- 

## Grammar

    program = atoms
    atoms = atom [SEPARATOR atoms]
    atom = COMMENT
    atom = statement
    statement = NAME ATTRIBUTE_START [attributes] ATTRIBUTE_STOP [CHILD_START atoms CHILD_STOP]
    attributes = attribute [ATTRIBUTE_SEPARATOR attributes]
    attribute = NAME ATTRIBUTE_ASSIGN value
    value = r'\'' TEXT r'\''
    value = NUMBER
    NUMBER = r'[0-9]+'
    NAME = r'[a-zA-Z][a-zA-Z0-9_-]*'
    COMMENT = COMMENT_START r'*\n'
    COMMENT_START = '\\'
    TEXT = r'^[\']'
    SEPARATOR = ROW_SEPARATOR
    SEPARATOR = COLUMN_SEPARATOR
    ATTRIBUTE_SEPARATOR = ','
    ROW_SEPARATOR = '\n'
    COLUMN_SEPARATOR = ','
    ATTRIBUTE_START = '('
    ATTRIBUTE_STOP = ')'
    ATTRIBUTE_ASSIGN = '='
    CHILD_START = '{'
    CHILD_STOP = '}'

### Grammar grammar

    program = atoms
    atoms = atom [NEWLINE atoms]
    atom = WORD EQUALS values
    values = value [values]
    value = WORD
    value = optional
    value = TEXT
    value = REGEX
    optional = OPTIONAL_START values OPTIONAL_STOP
    NEWLINE = '\n'
    WORD = r'[a-zA-Z_]+'
    EQUALS = '='
    OPTIONAL_START = '['
    OPTIONAL_STOP = ']'
    TEXT = TEXT_START WORDS TEXT_STOP
    TEXT_START = r'\''
    TEXT_STOP = r'\''
    WORDS = r'^[\']'
    REGEX = REGEX_START WORDS REGEX_STOP
    REGEX_START = r'r\''
    REGEX_STOP = r'\''

