# Meta model

## Composante

### Program
- entry: Bloc

### Bloc
- instrs: List(instr)

### arg
- variable
- valeurs
- operation

### Instruction
- appel // appel de fonction => list(arg) en entree => return valeurs s
- action
- affactation
- If: EClass
- Loop: EClass

### Loop
- cond: EBool
- bloc: Bloc

### IF
- cond: EBool
- ifBloc: Bloc
- elseBloc: Bloc

### param
- Nom: EString
- Type: Type

### Fonction
- Bloc: EClass // parametre c'est une liste variable
- TypeRet: Type
- Nom: EString
- params: List(Arg)

### Action
- direction : EClass // unitDist & distance | variable 
  => Dir (EEnum) + distance (EInt) + unitDistance
  => Dir => Horiz, Vert => negatif pour les arr et gauche
- rotation: EClass // unitRot & angle | variable 
  => angle + unit
- SetSpeed: Eclass
  => arg + unit
- getDistance: Eclass
  => unitDist en entree 
- clock: Eclass

// on est obligie d'init les variable a la decl
### Variable
- nom: EString
- valeur: EString | EInt | EDouble | ELong | Eboolean
- type: UnitDist | UnitDeg

### Type
- String
- Int
- Bool
- Long
- Double

### units EEnum
#### UnitDist
- cm 
- mm
#### UnitDeg
- radiant
- deg

### Operation
- BinOp: EOperation
- UnOp: EOperation

### op (EEnum)


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


### Expression (EClass, abstract)

### ArithUnaryExpr (EClass) extends Expression
- op: ArithUnaryOp
- operand: Expression [1] (containment)

### LogicUnaryExpr (EClass) extends Expression
- op: LogicUnaryOp
- operand: Expression [1] (containment)

### ArithBinaryExpr (EClass) extends Expression
- op: ArithBinaryOp
- left: Expression [1] (containment)
- right: Expression [1] (containment)

### LogicBinaryExpr (EClass) extends Expression
- op: LogicBinaryOp
- left: Expression [1] (containment)
- right: Expression [1] (containment)

### CompareExpr (EClass) extends Expression
- op: CompareOp
- left: Expression [1] (containment)
- right: Expression [1] (containment)