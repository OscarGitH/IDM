# Meta model

## Structure

### Program (EClass)
- fonctions: Fonction [0..*] (containment)
- entry: Bloc [1] (containment)

### Bloc (EClass)
- instrs: Instruction [0..*] (containment)

### Fonction (EClass)
- nom: EString
- typeRet: Type
- params: Param [0..*] (containment)
- bloc: Bloc [1] (containment)


## Variables

### Variable (EClass, abstract)
- nom: EString
- type: Type

### Param (EClass) extends Variable

// on est obligé d'init les variables à la décl
### VarDecl (EClass) extends Variable, Instruction
- init: Expression [1] (containment)


## Instructions

### Instruction (EClass, abstract)

### Affectation (EClass) extends Instruction
- variable: Variable [1] (référence)
- valeur: Expression [1] (containment)

### If (EClass) extends Instruction
- cond: BoolExpression [1] (containment)
- ifBloc: Bloc [1] (containment)
- elseBloc: Bloc [0..1] (containment)

### Loop (EClass) extends Instruction
- cond: BoolExpression [1] (containment)
- bloc: Bloc [1] (containment)

### Return (EClass) extends Instruction
- valeur: Expression [0..1] (containment)

### Appel (EClass) extends Instruction, Expression
- fonction: Fonction [1] (référence)
- args: Expression [0..*] (containment)


## Actions du robot

### Action (EClass, abstract) extends Instruction

// distance négative => arrière (VERT) ou gauche (HORIZ)
### Deplacement (EClass) extends Action
- dir: Direction
- distance: Expression [1] (containment)
- unit: UnitDist

### Clock (EClass) extends Action
- angle: Expression [1] (containment)
- unit: UnitDeg

### SetSpeed (EClass) extends Action
- vitesse: Expression [1] (containment)
- unit: UnitDist

// capteurs : renvoient une valeur => ce sont des expressions
### GetDistance (EClass) extends Expression
- unit: UnitDist

## Expressions

### Expression (EClass, abstract)

// expressions dont le résultat est un booléen (utilisables comme condition de If / Loop)
### BoolExpression (EClass, interface) extends Expression

### VarRef (EClass) extends Expression
- variable: Variable [1] (référence)

### IntLiteral (EClass) extends Expression
- valeur: EInt

### LongLiteral (EClass) extends Expression
- valeur: ELong

### DoubleLiteral (EClass) extends Expression
- valeur: EDouble

### BoolLiteral (EClass) extends BoolExpression
- valeur: EBoolean

### StringLiteral (EClass) extends Expression
- valeur: EString

### ArithUnaryExpr (EClass) extends Expression
- op: ArithUnaryOp
- operand: Expression [1] (containment)

### LogicUnaryExpr (EClass) extends BoolExpression
- op: LogicUnaryOp
- operand: BoolExpression [1] (containment)

### ArithBinaryExpr (EClass) extends Expression
- op: ArithBinaryOp
- left: Expression [1] (containment)
- right: Expression [1] (containment)

### LogicBinaryExpr (EClass) extends BoolExpression
- op: LogicBinaryOp
- left: BoolExpression [1] (containment)
- right: BoolExpression [1] (containment)

### CompareExpr (EClass) extends BoolExpression
- op: CompareOp
- left: Expression [1] (containment)
- right: Expression [1] (containment)


## Enums

### Type (EEnum)
- STRING
- INT
- BOOL
- LONG
- DOUBLE
- VOID         // pour les fonctions sans retour

### Direction (EEnum)
- HORIZ
- VERT

### UnitDist (EEnum)
- CM
- MM

### UnitDeg (EEnum)
- RADIAN
- DEG

### ArithUnaryOp (EEnum)
- NEG          // -x
- PLUS         // +x

### LogicUnaryOp (EEnum)
- NOT          // !x

### ArithBinaryOp (EEnum)
- ADD          // a + b
- SUB          // a - b
- MUL          // a * b
- DIV          // a / b
- MOD          // a % b

### LogicBinaryOp (EEnum)
- AND          // a && b
- OR           // a || b
- XOR          // a ^ b

### CompareOp (EEnum)
- EQ           // a == b
- NEQ          // a != b
- LT           // a < b
- LE           // a <= b
- GT           // a > b
- GE           // a >= b