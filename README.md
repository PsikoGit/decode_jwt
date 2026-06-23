J'ai développé un script bash permettant de décoder les token JWT, des outils beaucoup plus robustes existent comme le site [https://www.jwt.io/] mais j'ai tenu à faire ce code pour m'entraîner en scripting bash :

```bash
#!/bin/bash

if [[ $1 == "-h" || $1 == "--help" ]] ; then
    echo "Syntaxe d'utilisation :"
    echo "Utiliser l'option -f ou --filename en spécifiant le fichier contenant le token JWT"
    echo "Ou alors mettez en argument du script le token directement"
    echo ""
    echo "Exemple :"
    echo "./decode_jwt.sh -f token.txt"
    echo "./decode_jwt.sh --filename jwt.txt"
    echo "./decode_jwt.sh eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2Vy..."
    exit 0
fi


if [[ $1 == "-f" || $1 == "--filename" ]] ; then

    if [ -f "$2" ] ; then

        file_content=$(cat $2)

        for i in {1..3} ; do
            jwt_part=$(echo $file_content | cut -d '.' -f$i | base64 -d)
            echo "Champs n°$i : $jwt_part"
        done

    else
        echo "fichier vide"
        exit 1
    fi

else
    for i in {1..3} ; do
        jwt_part=$(echo "$1" | cut -d '.' -f$i | base64 -d)
        echo "Champs n°$i : $jwt_part"
    done
fi
```
