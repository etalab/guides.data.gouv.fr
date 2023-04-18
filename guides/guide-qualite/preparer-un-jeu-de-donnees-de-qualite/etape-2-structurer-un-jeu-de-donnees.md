# Etape 2 : Structurer un jeu de données

{% hint style="info" %}
Les jeux de données qui ont vocation à circuler seront réutilisés par des acteurs tiers qui ne connaissent pas l’environnement de votre organisation. Il est nécessaire de proposer une structure de jeu de données compréhensible et appropriable par tous.
{% endhint %}

Deux approches sont possibles :&#x20;

* **Cas 1 : La structure de vos données ne correspond pas à aucun schéma de données existant**. Un travail de modélisation est nécessaire en amont de la création du jeu de données.
* **Cas 2 : La structure de vos données correspond à un schéma de données existant** ;

{% tabs %}
{% tab title="Cas 1" %}
## Cas 1 - La structure de vos données ne correspond à aucun schéma de données existant <a href="#cas-2-la-structure-de-vos-donnees-ne-correspond-a-aucun-schema-de-donnees-existant" id="cas-2-la-structure-de-vos-donnees-ne-correspond-a-aucun-schema-de-donnees-existant"></a>

Il est nécessaire de réfléchir en amont à la meilleure structure pour vos données.

Tant que les données de votre administration sont dans un environnement logiciel, leur usage reste adapté à des problématiques métiers spécifiques.&#x20;

L’ouverture de ces données en dehors de leur environnement impose alors de **structurer le jeu de données en fonction des attentes des réutilisateurs** et non plus en fonction des besoins propres à l’organisation.

### Soigner le contenu du jeu de données <a href="#le-contenu-du-jeu" id="le-contenu-du-jeu"></a>

#### Les champs du jeu de données <a href="#le-titre-du-jeu-de-donnees" id="le-titre-du-jeu-de-donnees"></a>

Quelques bonnes pratiques à mettre en place :&#x20;

* [ ] **Occulter l’ensemble des colonnes dont les champs contiennent des données couvertes par un secret légal** (cf. [guide juridique](https://guides.etalab.gouv.fr/juridique)) ;
* [ ] **Occulter l’ensemble des colonnes dont les champs contiennent des données à caractère personnel** dont la publication n’est pas nécessaire à l’information du public (cf. [guide juridique](https://guides.etalab.gouv.fr/juridique)) ;
* [ ] **Privilégier la présence de variables pivots**. Ces variables proposent des identifiants communs qui permettent de lier plusieurs jeux de données entre eux (ex. le numéro d’identification SIRET de la base Sirene) (cf. page [Lier les données à un référentiel](https://guides.etalab.gouv.fr/qualite/lier-les-donnees-a-un-referentiel)).

#### Le titre du jeu de données <a href="#le-titre-du-jeu-de-donnees" id="le-titre-du-jeu-de-donnees"></a>

Le titre de votre jeu de données doit pouvoir renseigner n’importe quel réutilisateur sur le contenu du fichier. Pour cela, il est nécessaire de :&#x20;

* [ ] **Ne pas donner un titre trop générique** qui obligerait le réutilisateur à ouvrir le jeu de données pour comprendre son contenu (Par exemple “liste.csv” ou encore “balance comptable” sans indiquer l’organisation concernée) ;
* [ ] **Ne pas donner un titre trop long** qui rendrait la manipulation du fichier difficile. Par exemple le titre du jeu de données “Fichiers consolidés des données essentielles de la commande publique” est suffisamment générique pour ne pas revenir sur toutes les sources de données utilisées pour agréger le jeu de données ;
* [ ] **Ne pas donner un titre contenant des accents ou caractères spéciaux** qui poseraient des problèmes d’interopérabilité des fichiers ;
* [ ] **Ne pas donner de titre trop technique** issu de nomenclatures métier.

#### L’encodage du fichier <a href="#l-encodage-du-fichier" id="l-encodage-du-fichier"></a>

{% hint style="info" %}
L’encodage d’un fichier est la norme utilisée pour coder chaque caractère par une suite de 0 et de 1 compréhensible par une machine. Lorsque l’encodage est mal choisi, le réutilisateur des données est souvent contraint de convertir le fichier, notamment afin de faire apparaître les accents et caractères spéciaux.
{% endhint %}

**Il est conseillé d’utiliser l’encodage UTF-8**. Il permet d’encoder l’ensemble des caractères du répertoire universel de caractères codés (notamment les caractères contenants des accents ou des caractères spéciaux).

#### L’entête des colonnes (pour le format tabulaire) <a href="#l-entete-des-colonnes-pour-le-format-tabulaire" id="l-entete-des-colonnes-pour-le-format-tabulaire"></a>

{% hint style="info" %}
Dans un fichier tabulaire, la première ligne du fichier peut être utilisée pour nommer chaque colonne et donner des informations sur les données associées.&#x20;
{% endhint %}

* Il est conseillé de donner **un nom de colonne explicite**.&#x20;
* Le nom des colonnes doit être **sans majuscule, abréviation, accents, ni espaces** (préférez le caractère `_`) afin de faciliter la manipulation des fichiers.

#### Le séparateur (pour le format tabulaire) <a href="#le-separateur-pour-le-format-tabulaire" id="le-separateur-pour-le-format-tabulaire"></a>

{% hint style="info" %}
Dans un fichier tabulaire, le séparateur permet de structurer les données sous forme de cellules.&#x20;
{% endhint %}

Il est conseillé d’**utiliser la virgule comme séparateur**.

{% hint style="warning" %}
**Séparateurs décimaux**

Dans un fichier CSV, la virgule n’est pas considérée comme un séparateur décimal. Si votre fichier contient des valeurs décimales, il est nécessaire d’encapsuler chaque champ entre des guillemets. La plupart des tableurs (Excel, OpenOffice Calc, etc) proposent l’encapsulement des champs entre guillemets. Une seconde solution consiste à convertir l’ensemble des virgules utilisées pour des valeurs décimales par un point.
{% endhint %}

#### Gestion des champs non attribués <a href="#gestion-des-champs-non-attribues" id="gestion-des-champs-non-attribues"></a>

Il est possible que certaines occurrences d’un champ d'un fichier ne soit pas attribuées.&#x20;

Il convient de **laisser ces occurrences vides plutôt que d’attribuer la valeur 0** (ou une autre valeur par défaut). Le zéro correspond à une valeur, qui peut dénaturer le sens de votre fichier.

#### Granularité du jeu de données

Il est important de mener une réflexion sur la granularité du jeu de données.

Faut-il proposer des données fines ou agrégées ? Faut-il proposer un export quotidien, mensuel, trimestriel ou annuel ? Ces questions doivent être posées en amont de l’automatisation des exports.&#x20;

**Un dialogue avec les réutilisateurs est conseillé afin de comprendre leurs besoins**. Certains utilisateurs peuvent souhaiter manipuler des données granulaires tandis que d’autres préfèrent disposer d’agrégats qui permettent une réutilisation simple et rapide. A minima, il est conseillé de proposer un fichier complet unique qui contient l’ensemble des données historiques.

### Choisir le format du jeu de données <a href="#le-choix-du-format-du-jeu-de-donnees" id="le-choix-du-format-du-jeu-de-donnees"></a>

Afin qu'un maximum d’utilisateurs puisse s’approprier les données, il est conseillé de les faire circuler dans un format :

* **Ouvert** : un format ouvert n’impose pas de spécifications techniques qui entraveraient l’exploitation des données (par exemple l’utilisation d’un logiciel payant) ;
* **Aisément réutilisable** : un format aisément réutilisable sous-entend que toute personne ou machine peut réutiliser facilement le jeu de données ;
* **Exploitable par un système de traitement automatisé** : un système de traitement automatisé permet de réaliser des opérations par des moyens automatiques, relatifs à l’exploitation des données. Par exemple, un fichier CSV est aisément exploitable par un système de traitement automatisé contrairement à un fichier PDF.

Les formats ouverts et communément acceptés sont les suivants :&#x20;

| Type de données                | Formats conseillés                                                                                                                          | Documentation                                                                                                                     | Description                                                                                                                                                                                                                             |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Données tabulaires             | CSV                                                                                                                                         | [Ici](https://opendatafrance.gitbook.io/odl-ressources/fiches-pratiques/premiers-pas/produire-un-fichier-csv-de-qualite#contexte) | Un fichier CSV est constitué de lignes de données, où chaque champ est séparé par une virgule. Ce format est le standard le plus réutilisable, car ouvert et facilement exploitable par une machine.                                    |
| Données statiques de transport | GTFS/NeTEx                                                                                                                                  | [Ici](https://transport.data.gouv.fr/guide)                                                                                       | Le format GTFS est le format le plus utilisé en France par les services de mobilité d’information voyageur. Le format NeTEx est le format de référence européen qui vise l’interopérabilité des données entre États membres.            |
| Données géographiques          | GeoJSON, Shapefile, MapInfo MIF/MID, MapInfo TAB et GML, pour les vecteurs / ECW, JPEG2000 et GeoTIFF, pour les données pixelisées (raster) | [Ici](https://geo.data.gouv.fr/fr/doc/publish-your-data)                                                                          | Les données géographiques sont organisées sous forme d’ensemble de données hiérarchisées. Les formats proposés sont conçus spécifiquement pour être largement exploitables et être intégrés facilement dans des outils de cartographie. |
| Données hiérarchiques          | JSON / XML / YAML                                                                                                                           | indisponible                                                                                                                      | Les données hiérarchiques décrivent des relations hiérarchiques entre différentes données. Le format JSON est préconisé lorsque les données sont liées entre elles sous forme d’arbres verticaux.                                       |
{% endtab %}

{% tab title="Cas 2" %}
## Cas 2 - La structure des données correspond à un schéma de données existant

{% hint style="info" %}
**Lexique : Schéma de données**

Un schéma de données est un document qui permet de décrire de manière précise et univoque les différents champs et valeurs possibles qui composent un fichier.

Il permet notamment de valider qu’un fichier est conforme à une structure communément partagée, de générer de la documentation automatiquement, de générer des jeux de données d’exemple ou de proposer des formulaires de saisie standardisés. Ces schémas facilitent la montée en qualité et le croisement des données proposées en open data, surtout lorsque plusieurs producteurs de données sont amenés à produire un même jeu de données.



➡️ Consultez [notre guide à destination des producteurs de schémas](https://guides.etalab.gouv.fr/producteurs-schemas/)



Les schémas existants peuvent avoir été définis par voie :

* **Réglementaire** : un modèle de données a été défini de manière réglementaire, par décret ou arrêté. Un schéma est un moyen de faciliter l’adoption de ces modèles par les producteurs de données. Par exemple, le schéma de données relatif à la publication des données essentielles dans la commande publique est fixé par [arrêté depuis le 14 avril 2017](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000034492587\&categorieLien=id).
* **D’usage** : la réutilisation des données décrites par le schéma bénéficie à un grand nombre de réutilisateurs et aux nombreux producteurs utilisant ce schéma.
{% endhint %}

### **Identifier un schéma de données déjà existant**

Le site [schema.data.gouv.fr](http://schema.data.gouv.fr/) référence une liste de schémas de données existants. Il offre aussi la possibilité à tout utilisateur de soumettre de nouveaux schémas de données.&#x20;

Lorsque les données que vous souhaitez faire circuler correspondent à un schéma existant, nous vous conseillons de l’appliquer au plus près.

### **Produire des données conforme à un schéma de données identifié**

Si les données ne sont pas extraites d’un système d’information mais saisies manuellement, **nous vous conseillons d'utiliser** [**l’outil publier.etalab.studio**](https://publier.etalab.studio/) qui permet, à partir d’un schéma de données sélectionné, de saisir les valeurs de chaque information et ainsi de produire un fichier exhaustif et conforme.

{% hint style="info" %}
Cet outil vous permet de créer un fichier CSV en vous assurant qu'il est conforme à un schéma, c'est-à-dire que ses données sont complètes, valides et structurées.

1. **Sélectionnez le schéma** qui vous intéresse dans la liste déroulante (les schémas disponibles sont ceux référencés sur [schema.data.gouv.fr](https://schema.data.gouv.fr/)).
2. **Remplissez le formulaire** à l'aide des descriptions des différents champs et des valeurs d'exemples. Les champs indiqués par un astérisque rouge doivent obligatoirement être renseignés au moment de la saisie.
3. L'outil vous prévient d'éventuelles erreurs de validation, le cas échéant vous pouvez les corriger.
4. Une fois votre formulaire valide, les valeurs apparaissent sous la forme d'une ligne dans un tableau récapitulatif.
5. **Vous pouvez alors choisir d'ajouter une ou plusieurs lignes** (répétez les étapes 2 à 4) ou **télécharger le fichier CSV correspondant au tableau récapitulatif**.
{% endhint %}

### **Valider la conformité d’un fichier avec un schéma de données**

Il est possible de valider la conformité d’un fichier à un schéma de données existant grâce à différents outils.

**Avec la solution** [**Validata**](https://validata.fr/), vous pouvez valider la conformité de votre fichier à un schéma parmi la liste déroulante ou via une URL. Vous pouvez ensuite faire valider ce fichier, soit en l'important au format csv, soit en renseignant également son URL.

![Capture d'écran du menu de validata](https://guides.etalab.gouv.fr/assets/img/validata.f6a9dd72.png)

Tout d'abord, il est possible d'indiquer que votre fichier correspond à un schéma depuis l'interface d'administration de data.gouv.fr. Lorsque vous déposez ou éditez une ressource, vous pouvez sélectionner le schéma correspondant à vos données dans une liste déroulante.

![Capture d'écran de la sélection d'un schéma depuis l'interface d'administration de data.gouv.fr](https://guides.etalab.gouv.fr/assets/img/selection-schema.d958a2c6.png)

Le fait d'indiquer que votre ressource est censée respecter un schéma permet de bénéficier de vérifications de la qualité des données, d'indiquer aux réutilisateurs que vos données respectent un référentiel, ainsi que de contribuer aux fichiers agrégés (par exemple [pour les données IRVE](https://www.data.gouv.fr/fr/datasets/fichier-consolide-des-bornes-de-recharge-pour-vehicules-electriques/)).

![Capture d'écran de data.gouv.fr des informations disponibles sur la page d'un jeu de données lorsqu'un schéma est spécifié sur une ressource](https://guides.etalab.gouv.fr/assets/img/modal-schema.7ecaa269.png)

D'autres solutions en dehors de data.gouv.fr existent. Des solutions disponibles en anglais comme [goodtables.io](http://goodtables.io/) ou [CSV Lint](https://csvlint.io/) proposent des validateurs de jeux de données. Enfin, il est possible d’intégrer une fonction de validation d’un jeu directement dans la procédure de publication. C’est le cas pour les données d’adresses locales qui font l’objet d’une validation directement sur le site [adresse.data.gouv.fr](https://adresse.data.gouv.fr/).
{% endtab %}
{% endtabs %}


