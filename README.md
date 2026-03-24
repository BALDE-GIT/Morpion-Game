 morpion.c
#include <stdio.h>

int main(void) {
    char grille[4][4];
    int i, j;
    int ligne, colonne;
    int tour;
    int joue;

    printf("Jeu du morpion 4x4\n");
    printf("Joueur = X, Ordinateur = O\n\n");

    /* Initialiser la grille avec des espaces (cases vides) */
    for (i = 0; i < 4; i++) {
        for (j = 0; j < 4; j++) {
            grille[i][j] = ' ';
        }
    }

    /* Boucle de jeu : plusieurs tours */
    for (tour = 0; tour < 4; tour++) {

        /* ----- Coup du joueur X ----- */
        printf("Tour %d - Joueur (X)\n", tour + 1);
        printf("Entrez la ligne (0-3) : ");
        scanf("%d", &ligne);
        printf("Entrez la colonne (0-3) : ");
        scanf("%d", &colonne);

        /* Verifier que le coup est dans la grille et que la case est libre */
        if (ligne >= 0 && ligne < 4 && colonne >= 0 && colonne < 4) {
            if (grille[ligne][colonne] == ' ') {
                grille[ligne][colonne] = 'X';
            } else {
                printf("Case deja occupee.\n");
            }
        } else {
            printf("Coordonnees invalides.\n");
        }

        /* Afficher la grille apres le coup du joueur */
        printf("Grille apres le coup du joueur :\n");
        for (i = 0; i < 4; i++) {
            for (j = 0; j < 4; j++) {
                printf("|%c", grille[i][j]);
            }
            printf("|\n");
        }

        /* ----- Coup simple de l'ordinateur O ----- */
        printf("Tour %d - Ordinateur (O)\n", tour + 1);

        joue = 0;
        for (i = 0; i < 4 && !joue; i++) {
            for (j = 0; j < 4 && !joue; j++) {
                if (grille[i][j] == ' ') {
                    grille[i][j] = 'O';
                    joue = 1;
                }
            }
        }

        /* Afficher la grille apres le coup de l'ordinateur */
        printf("Grille apres le coup de l'ordinateur :\n");
        for (i = 0; i < 4; i++) {
            for (j = 0; j < 4; j++) {
                printf("|%c", grille[i][j]);
            }
            printf("|\n");
        }
    }

    /* Compter les X et les O pour afficher un gagnant simple */
    int nbX = 0;
    int nbO = 0;

    for (i = 0; i < 4; i++) {
        for (j = 0; j < 4; j++) {
            if (grille[i][j] == 'X') {
                nbX++;
            } else if (grille[i][j] == 'O') {
                nbO++;
            }
        }
    }

    printf("Nombre de X : %d\n", nbX);
    printf("Nombre de O : %d\n", nbO);

    if (nbX > nbO) {
        printf("Le joueur gagne.\n");
    } else if (nbO > nbX) {
        printf("L'ordinateur gagne.\n");
    } else {
        printf("Egalite.\n");
    }

    return 0;
}
