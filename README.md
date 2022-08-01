# 7.3 // Generalização, Especialização e Polimorfismo // Matrix

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <https://classroom.github.com/a/1E8RN170>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** generalização, super classes, classes abstratas, especialização, classes concretas e polimorfismo.

---

Implementar a Matrix

Considere a Matrix e todos os relacionamentos. Implemente conforme os casos de teste a seguir. Para uma melhor experiência, [assista o filme](https://www.imdb.com/title/tt0133093/).


```java
Matrix matrix = Matrix.get(); // `get` é um método estático.

// Esta linha não deve compilar, só há UMA Matrix, `new` não permitido.
Matrix matrix2 = new Matrix(); // comente após fazê-la quebrar.

// Get não retorna novas Matrix, mas sempre a mesma.
System.out.println(matrix       == Matrix.get());
System.out.println(Matrix.get() == Matrix.get());

// Algumas pessoas nascem na Matrix.
Human Neo    = matrix.newHuman("Anderson", "Tomas"); // sobrenome e nome
Human Dujour = matrix.newHuman("Dujour"); // apelido
Human Paul   = matrix.newHuman("Olsen", "Paul");
Human Kid    = matrix.newHuman("Popper", "Karl", "Michael"); // sobrenome, segundo nome, nome
==
// Assim como há programas
Program Oracle      = matrix.newProgram("Oracle"); // apelido
Program Merovingian = matrix.newProgram("Merovingian"); // apelido

// Esta linha não deve compilar,
// pois programas só podem ser instanciados dentro da Matrix.
Program program = new Program("program");

// Também existem agentes na Matrix.
Agent Smith = matrix.newAgent("Smith"); // Lastname
Agent Brown = matrix.newAgent("Brown"); // Lastname

// Esta linha não deve compilar, pois agentes são como os programas.
Agent agent = new Agent("agent");

// Algumas pessoas estão fora da matrix.
Human Trinity  = new Human("Trinity");
Human Morpheus = new Human("Morpheus");
Human Mouse    = new Human("Mouse");
Human Dozer    = new Human("Dozer");
Human Roland   = new Human("Roland");
Human Niobe    = new Human("Niobe");
Human Apoc     = new Human("Apoc");
Human Cypher   = new Human("Cypher");
Human Ghost    = new Human("Ghost");
Human Sparks   = new Human("Sparks");

// Existem hovercrafts ou naves.
Ship Nebuchadnezzar = new Ship("Nebuchadnezzar");
Ship Logos          = new Ship("Logos");
Ship Mjolnir        = new Ship("Mjolnir");

System.out.println(Neo.getFirstName().equals("Tomas"));
System.out.println(Neo.getLastName() .equals("Anderson"));
System.out.println(Neo.getFullName() .equals("Tomas Anderson"));
System.out.println(Neo.toString()    .equals("Mr. Anderson")); // Mr Lastname
System.out.println(Neo.getAlias() == null); // Neo não tem alias ainda

System.out.println(Oracle.getFirstName() == null);
System.out.println(Oracle.getLastName()  == null);
System.out.println(Oracle.getFullName()  == null);
System.out.println(Oracle.getAlias().equals("Oracle"));
System.out.println(Oracle.toString().equals("The Oracle")); // The Alias, quando é um Programa

System.out.println(Paul.getFirstName().equals("Paul"));
System.out.println(Paul.getLastName() .equals("Olsen"));
System.out.println(Paul.getFullName() .equals("Paul Olsen"));
System.out.println(Paul.toString()    .equals("Mr. Olsen")); // Mr Lastname
System.out.println(Paul.getAlias() == null); // Paul não têm alias

System.out.println(Kid.getFirstName() .equals("Michael"));
System.out.println(Kid.getLastName()  .equals("Popper"));
System.out.println(Kid.getMiddleName().equals("Karl"));
System.out.println(Kid.getFullName()  .equals("Michael Karl Popper"));
System.out.println(Kid.toString()     .equals("Mr. Popper")); // Mr Lastname
System.out.println(Kid.getAlias() == null); // Kid não têm alias, ainda

System.out.println(Smith.getFirstName() == null);
System.out.println(Smith.getFullName()  == null);
System.out.println(Smith.getAlias()     == null);
System.out.println(Smith.getLastName().equals("Smith"));
System.out.println(Smith.toString()   .equals("Agent Smith")); // Agent Alias, quando é um Agente

System.out.println(Trinity.getFirstName() == null);
System.out.println(Trinity.getLastName()  == null);
System.out.println(Trinity.getFullName()  == null);
System.out.println(Trinity.getAlias().equals("Trinity"));
System.out.println(Trinity.toString().equals("Trinity")); // Só o alias quando a pessoa tem um

// Estão ou não na Matrix.
System.out.println(Neo     .isPlugged() == true); // Neo está na Matrix
System.out.println(Dujour  .isPlugged() == true);
System.out.println(Smith   .isPlugged() == true);
System.out.println(Morpheus.isPlugged() == false); // Morpheus não está.

System.out.println(matrix.has(Neo)      == true); // A Matrix tem Neo.
System.out.println(matrix.has(Dujour)   == true);
System.out.println(matrix.has(Oracle)   == true);
System.out.println(matrix.has(Morpheus) == false); // Mas não tem Morpheus.
System.out.println(matrix.has(Trinity)  == false);

// Libertando-se da Matrix
matrix.free(Neo, "Neo"); // ao sair da matrix as pessoas ganham um apelido e não tem mais nome

System.out.println(Neo.isPlugged()    == false); // Neo não está na Matrix
System.out.println(matrix.has(Neo)    == false); // Nem a Matrix tem Neo

System.out.println(Neo.getFirstName() == null); // Temporário até ele voltar
System.out.println(Neo.getLastName()  == null); // Temporário até ele voltar
System.out.println(Neo.getFullName()  == null); // Temporário até ele voltar
System.out.println(Neo.getAlias().equals("Neo"));
System.out.println(Neo.toString().equals("Neo"));

matrix.free(Smith, "Smith"); // Smith é um Agente e não pode ser libertado

System.out.println(Smith.isPlugged() == true);
System.out.println(matrix.has(Smith) == true);

// A Nave está vazia
System.out.println(Nebuchadnezzar.crewCount()  == 0);
System.out.println(Nebuchadnezzar.getCaptain() == null);
// Até ser tripulada.
Nebuchadnezzar.recruit(Trinity); // recrutar tripulação
// O primeiro a entrar é o capitão
System.out.println(Nebuchadnezzar.crewCount() == 1);
System.out.println(Nebuchadnezzar.getCaptain().equals(Trinity) == true);

Nebuchadnezzar.recruit(Morpheus);
Nebuchadnezzar.recruit(Mouse);
Nebuchadnezzar.recruit(Dozer);
Nebuchadnezzar.recruit(Neo);

System.out.println(Nebuchadnezzar.crewCount() == 5);

// só se for membro da tripulação, Niobe não é!
Nebuchadnezzar.promoteToCaptain(Niobe);
System.out.println(Nebuchadnezzar.getCaptain().equals(Trinity) == true);
System.out.println(Trinity.isCaptainOf(Nebuchadnezzar)         == true);
System.out.println(Niobe.isCaptainOf(Nebuchadnezzar)           == false);

// Morpheus é o Capitão agora
Nebuchadnezzar.promoteToCaptain(Morpheus);

System.out.println(Nebuchadnezzar.getCaptain().equals(Morpheus) == true);
System.out.println(Nebuchadnezzar.getCaptain().equals(Niobe)    == false);
System.out.println(Niobe.isCaptainOf(Nebuchadnezzar)            == false);
System.out.println(Trinity.isCaptainOf(Nebuchadnezzar)          == false);
System.out.println(Nebuchadnezzar.getCaptain().equals(Trinity)  == false);

System.out.println(Morpheus.isCaptainOf(Nebuchadnezzar) == true);

// Populando a Logos
System.out.println(Logos.crewCount() == 0);
Logos.recruit(Ghost);
Logos.recruit(Niobe);
Logos.recruit(Sparks);
System.out.println(Logos.crewCount() == 3);

System.out.println(Logos.getCaptain().equals(Ghost) == true);
System.out.println(Ghost.isCaptainOf(Logos)         == true);
System.out.println(Logos.getCaptain().equals(Niobe) == false);

Niobe.promoteToCaptainOf(Logos);

System.out.println(Logos.getCaptain().equals(Niobe) == true);
System.out.println(Niobe.isCaptainOf(Logos)         == true);

System.out.println(Nebuchadnezzar.crewCount() == 5);
System.out.println(Logos.crewCount()          == 3);

System.out.println(Mouse.isCrewMemberOf(Nebuchadnezzar) == true);
System.out.println(Mouse.isCrewMemberOf(Logos)          == false);
System.out.println(Niobe.isCrewMemberOf(Nebuchadnezzar) == false);
System.out.println(Niobe.isCrewMemberOf(Logos)          == true);

Logos.recruit(Mouse); // não pode pois já é membro da Nebuchadnezzar

System.out.println(Mouse.isCrewMemberOf(Nebuchadnezzar) == true);
System.out.println(Mouse.isCrewMemberOf(Logos)          == false);

System.out.println(Nebuchadnezzar.crewCount() == 5);
System.out.println(Logos.crewCount()          == 3);

// um tripulante pode ser dispensado
Nebuchadnezzar.dismiss(Mouse);

System.out.println(Nebuchadnezzar.crewCount() == 4);
System.out.println(Logos.crewCount()          == 3);

Logos.recruit(Mouse);

System.out.println(Nebuchadnezzar.crewCount() == 4);
System.out.println(Logos.crewCount()          == 4);

System.out.println(Mouse.isCrewMemberOf(Nebuchadnezzar) == false);
System.out.println(Mouse.isCrewMemberOf(Logos)          == true);

Mouse.resign(); // outro modo de deixar de ser membro de uma tripulação

System.out.println(Nebuchadnezzar.crewCount() == 4);
System.out.println(Logos.crewCount()          == 3);

System.out.println(Mouse.isCrewMemberOf(Nebuchadnezzar) == false);
System.out.println(Mouse.isCrewMemberOf(Logos)          == false);

Mouse.join(Nebuchadnezzar); // outro modo de tornar-se tripulação
Mouse.join(Logos); // rejeitado, não pode se juntar à duas naves, vale a primeira

System.out.println(Mouse.isCrewMemberOf(Nebuchadnezzar) == true);
System.out.println(Mouse.isCrewMemberOf(Logos)          == false);
System.out.println(Nebuchadnezzar.crewCount()           == 5);
System.out.println(Logos.crewCount()                    == 3);
System.out.println(Nebuchadnezzar.getCaptain().equals(Morpheus));

Mouse.join(Nebuchadnezzar); // não pode juntar-se duas vezes
Logos.recruit(Mouse); // rejeitado, não pode se juntar à duas naves, vale a primeira

System.out.println(Nebuchadnezzar.crewCount() == 5);
System.out.println(Logos         .crewCount() == 3);

matrix.enter(Neo); // Neo entra na matrix
matrix.enter(Morpheus); // Morpheus também
matrix.enter(Trinity, Mouse); // duas pessoas podem entrar juntas

System.out.println(Neo.isPlugged()      == true);
System.out.println(Morpheus.isPlugged() == true);
System.out.println(matrix.has(Trinity)  == true);
System.out.println(matrix.has(Mouse)    == true);

// A qualquer momento pode ser obtida a Matrix pelo método estático `get()`
Matrix.get().leave(Morpheus); // Um pode sair da Matrix atráves do método leave

System.out.println(Morpheus.isPlugged() == false);

Morpheus.plug(); // outro modo de entrar na matrix

System.out.println(Morpheus.isPlugged() == true);

Morpheus.unplug(); // outro modo de sair da matrix

System.out.println(Morpheus.isPlugged() == false);
System.out.println(Morpheus.isAlive()   == true); // Está vivo!
System.out.println(Apoc    .isPlugged() == false);

Cypher.unplug(Apoc); // uma pessoa pode desplugar outra, mas Apoc não está plugado
System.out.println(Apoc.isAlive()       == true);
Apoc.plug(); // Apoc entrou na Matrix
System.out.println(Apoc.isPlugged()     == true);
Cypher.unplug(Apoc); // desplugar alguém da Matrix é assassina-lo
System.out.println(Apoc.isPlugged()     == false);
System.out.println(Apoc.isAlive()       == false);
System.out.println(Dozer.isAlive()      == true);
Cypher.kill(Dozer);
System.out.println(Dozer.isAlive()      == false);
System.out.println(Roland.isAlive()     == true);
Smith.kill(Roland); // não pode, Smith está na Matrix e Roland não
System.out.println(Roland.isAlive()     == true);
System.out.println(Mouse.isAlive()      == true);
Smith.kill(Mouse); // ambos estão na Matrix, então Mouse é morto
System.out.println(Mouse.isAlive()      == false);
System.out.println(Mouse.isPlugged()    == false);
Dozer.kill(Cypher); // Dozer está morto então não pode fazer nada
System.out.println(Cypher.isAlive()     == true);
matrix.enter(Dozer) // Dozer estão morto
System.out.println(matrix.has(Dozer)    == false);

// caso especial: ⚠️ SPOILER ALERT!
Neo.kill(Smith); // Neo libertou, na verdade, Smith
System.out.println(Smith.isAlive()   == true);
System.out.println(Smith.isPlugged() == false);
System.out.println(matrix.has(Smith) == true);

System.out.println(Smith.is(Person.PROGRAM)       == true);
System.out.println(Smith.is(Person.AGENT)         == true);
System.out.println(Merovingian.is(Person.PROGRAM) == true);
System.out.println(Neo.is(Person.PROGRAM)         == false);
System.out.println(Neo.is(Person.HUMAN)           == true);

System.out.println(Merovingian.isPlugged() == true);
Merovingian.unplug(); // Só Humanos entram e saem da Matrix
System.out.println(Merovingian.isPlugged() == true);

System.out.println(Paul.isAlive()   == true);
Neo.kill(Paul); // se morreu, desplugou-se
System.out.println(Paul.isAlive()   == false);
System.out.println(Paul.isPlugged() == false);

System.out.println(Kid.isPlugged()  == true);

// Somente Neo tem o poder de libertar as pessoas da Matrix
Neo.free(Kid, "Kid");
System.out.println(Kid.isPlugged()     == false);
System.out.println(Kid.getFirstName()  == null);
System.out.println(Kid.getLastName()   == null);
System.out.println(Kid.getMiddleName() == null);
System.out.println(Kid.getFullName()   == null);
System.out.println(Kid.getAlias().equals("Kid"));
System.out.println(Kid.toString().equals("Kid"));

System.out.println(Niobe .isAlive() == true);
System.out.println(Ghost .isAlive() == true);
System.out.println(Sparks.isAlive() == true);

Logos.destroy(); // destruir o hovercraft implica em matar toda a tripulação
System.out.println(Niobe .isAlive() == false);
System.out.println(Ghost .isAlive() == false);
System.out.println(Sparks.isAlive() == false);
```
