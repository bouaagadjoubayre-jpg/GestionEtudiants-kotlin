
open class Personne(
    var nom: String,
    var prenom: String,
    var age: Int
)

enum class Statut {
    INTERN, EXTERN
}

class Etudiant(
    nom: String,
    prenom: String,
    age: Int,
    val cne: String,
    var statut: Statut
) : Personne(nom, prenom, age)

class GestionEtudiant(
    var etudiants: ArrayList<Etudiant> = arrayListOf()
) {
    fun addEtudiant(etudiant: Etudiant) {
        val existe = etudiants.any {
            it.cne == etudiant.cne
        }

        if (!existe) {
            etudiants.add(etudiant)
            println("Etudiant a ete ajoute")
        } else {
            println("Etudiant existe déjà")
        }
    } // نهاية addEtudiant

    fun removeEtudiant(cne: String) {
        val action = etudiants.removeIf {
            it.cne == cne
        }

        if (action) {
            println("Etudiant avec $cne est removed")
        } else {
            println("L'etudiant n'existe pas")
        }
    } // نهاية removeEtudiant

    fun affiche() {
        if (etudiants.isNotEmpty()) {
            etudiants.forEach {
                println(
                    "L'etudiant ${it.cne}, nom complet: " +
                            "${it.nom} ${it.prenom}, statut: ${it.statut}"
                )
            }
        } else {
            println("La liste d'etudiants est vide")
        }
    } // نهاية affiche

    fun isPresent(cne: String): Boolean {
        return etudiants.any {
            it.cne == cne
        }
    } // نهاية isPresent
}

fun main() {
    val gestion = GestionEtudiant()

    val et1 = Etudiant(
        "Bouagade", "Jobayr", 19, "123321", Statut.INTERN
    )

    val et2 = Etudiant(
        "bari", "Ahmed", 20, "761234", Statut.EXTERN
    )

    gestion.addEtudiant(et1)
    gestion.addEtudiant(et2)

    gestion.affiche()
    gestion.removeEtudiant("761234")
    gestion.affiche()
}
