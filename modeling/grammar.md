# GCM language grammar

The full grammar behind the GCM language is shown below:

```java
grammar GreyCatModel;

fragment ESC :   '\\' (["\\/bfnrt] | UNICODE) ;
fragment UNICODE : 'u' HEX HEX HEX HEX ;
fragment HEX : [0-9a-fA-F] ;

STRING :  '"' (ESC | ~["\\])* '"' | '\'' (ESC | ~["\\])* '\'' ;
IDENT : [a-zA-Z_][a-zA-Z_0-9]*;
NUMBER : [\-]?[0-9]+'.'?[0-9]*;
WS : ([ \t\r\n]+ | SL_COMMENT | ML_COMMENT) -> skip ; // skip spaces, tabs, newlines
SL_COMMENT :  '//' ~('\r' | '\n')* ;
ML_COMMENT : '/*' .*? '*/' -> skip;

modelDcl: (constDcl | classDcl | globalIndexDcl | customTypeDcl | importDcl)*;
importDcl: 'import' path=STRING;
constDcl: 'const' name=IDENT ':' type=IDENT ('=' constValueDcl)?;
constValueDcl: (simpleValueDcl | taskValueDcl);
simpleValueDcl: (IDENT | STRING | NUMBER);
taskValueDcl: actionValueDcl ('.' actionValueDcl)*;
actionValueDcl: IDENT ('(' actionParamList ')')?;
actionParamList: actionParam (',' actionParam)*;
actionParam: STRING | NUMBER | subTask;
subTask: '{' taskValueDcl '}';

classDcl: 'class' name=IDENT parentDcl? '{' (annotationDcl | constDcl | attributeDcl | relationDcl | referenceDcl | localIndexDcl)* '}';
customTypeDcl: 'type' name=IDENT parentDcl? '{' (constDcl | attributeDcl)* '}';

parentDcl: 'extends' IDENT;
attributeDcl: 'att' name=IDENT ':' type=IDENT ('=' attributeValueDcl)?;
annotationDcl: '@' name=IDENT ('=' value=attributeValueDcl)?;

attributeValueDcl: (IDENT | STRING | NUMBER | complexAttributeValueDcl);
complexAttributeValueDcl: '(' complexValueDcl (',' complexValueDcl)* ')';
complexValueDcl: (IDENT | STRING | NUMBER | ntupleValueDlc);
ntupleValueDlc: '(' ntupleElementDlc (',' ntupleElementDlc)* ')';
ntupleElementDlc: (IDENT | STRING | NUMBER);

relationDcl: 'rel' name=IDENT ':' type=IDENT (oppositeDcl)?;
referenceDcl: 'ref' name=IDENT ':' type=IDENT (oppositeDcl)?;
oppositeDcl: 'oppositeOf' name=IDENT;

localIndexDcl: 'index' name=IDENT ':' type=IDENT 'using' indexAttributesDcl (oppositeDcl)?;
indexAttributesDcl: IDENT (',' IDENT)*;

globalIndexDcl: 'index' name=IDENT ':' type=IDENT 'using' indexAttributesDcl;
```