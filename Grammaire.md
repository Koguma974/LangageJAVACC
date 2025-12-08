############ Terminaux / Types ############

String => Char String | €
Char => Lettre | Chiffre | Symbole
Lettre => A|B|C|D|E|F|G|H|I|J|K|L|M|N|O|P|Q|R|S|T|U|V|W|X|Y|Z|a|b|c|d|e|f|g|h|i|j|k|l|m|n|o|p|q|r|s|t|u|v|w|x|y|z
Chiffre => 0|1|2|3|4|5|6|7|8|9
Symbole => (espace)|!|"|#|$|%|&|'|(|)|*|+|,|-|.|/|:|;|<|=|>|?|@|[|\|]|^|_|`|{|}|~

Boolean => true | false
VariableLog => Boolean | Identifiant

Nombre => Int | Float
Int =>  Int Chiffre | Chiffre
Float => Int.Int
VariableArith => Nombre | Identifiant

Identifiant => Lettre SuiteIdentifiant
SuiteIdentifiant => Lettre SuiteIdentifiant | Chiffre SuiteIdentifiant | _ SuiteIdentifiant | €

Identifiant => (Lettre | Chiffre | _)+ // autant qu'on veut mais au moins 1 si on autorise de commencer par un chiffre--------


############ Listes ############

StringListe => [ EltString ]
EltString => String | String , EltString

FloatListe => [ EltFloat ]
EltFloat => Float | Float , EltFloat

IntListe => [ EltInt ]
EltInt => Int | Int , EltInt

BoolListe => [ EltBool ]
EltBool => Boolean | Boolean , EltBool

############ Logique ############

ExprLog => ExprLog or EltLog | EltLog
EltLog => EltLog and TermeLog | TermeLog
TermeLog => ValLog | !ValLog
ValLog => VariableLog | (ExprLog) | AppelFuncLog | Comp | Identifiant [ExprArith]

############ Comparaison ############

Comp => ExprArith OpComp ExprArith | ExprArith OpEq ExprArith |ExprString OpEq ExprString
OpEq => = | !=
OpComp => > | < | >= | <=

############ Arithmetique ############

ExprArith => ExprArith + EltArith | ExprArith - EltArith | EltArith
EltArith => EltArith * TermArith | EltArith / TermArith | TermArith
TermArith => -ValArith | ValArith
ValArith => VariableArith | AppelFuncArith | (ExprArith) | Identifiant [ExprArith]

############ Expressions générales ############

Expr => ExprArith | ExprLog | ExprString

ExprString => TermeString ExprStringSuite | Saisie
ExprStringSuite => + TermeString ExprStringSuite | €

ExprString => TermeString (+ TermeString)* // n termes string -------


TermeString => String | Identifiant | AppelFuncString | Nombre | (ExprArith) // nombre ou chiffre car chiffre dans string-----

############ Appels fonctions ############

AppelFuncArith => Identifiant ( ListeArgs )
AppelFuncLog => Identifiant ( ListeArgs )
AppelFuncString => Identifiant ( ListeArgs )
AppelProc => Identifiant ( ListeArgs )

ListeArgs => Expr | Expr , ListeArgs | €

############ Structure globale ############

Programme => ListeDeclarations ListeFonctionsEtProcs Main

ListeDeclarations => DeclarationVar ListeDeclarations | €
DeclarationVar => Type ListeIdentifiantVar ;
ListeIdentifiantVar => Identifiant | Identifiant , ListeIdentifiantVar

ListeFonctionsEtProcs => DeclarationFunc ListeFonctionsEtProcs | DeclarationProc ListeFonctionsEtProcs | €
DeclarationFunc => fun (Type) Identifiant (ListeParam) { ListeDeclarations ListeInstructions}
DeclarationProc => proc Identifiant (ListeParam) { ListeDeclarations ListeInstructions}

ListeParam => DeclarationParam ListeParamSuite | €
ListeParamSuite => , DeclarationParam ListeParamSuite | €
DeclarationParam => Type Identifiant

Main => main { ListeDeclarations ListeInstructions }

############ Instructions ############

ListeInstructions => Instruction ListeInstructions | €

Instruction => Affectation; | Si | TantQue | Retour; | AppelProc; | Affichage; | Bloc

Bloc => {ListeInstructions}

Affectation => NomVariable := Expr
NomVariable => Identifiant | Identifiant [ExprArith]

Si => if (ExprLog) Bloc Sinon
Sinon => else Bloc | €

TantQue => while (ExprLog) Bloc

Retour => return Expr

Affichage => print (Expr)

// Add input
Saisie => input()

############ Parametres ############

Type => int | float | string | boolean | int [] | float [] | string [] | boolean []

############  ############