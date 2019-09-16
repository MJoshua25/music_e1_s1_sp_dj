# Music

* **Categorie**
* **Artist**
* **Son**
* **Album**
* **Commentaire**

## Categorie

```python
class Categorie(models.Model):
    """Model definition for Categorie."""

    # TODO: Define fields here
    auteur = models.ForeignKey(User, on_delete=models.CASCADE)
    image = models.ImageField(upload_to='categorie/')
    titre = models.CharField(max_length=255)
    description = models.TextField()
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_now=True)
    statut = models.BooleanField(default=False)

    class Meta:
        """Meta definition for Categorie."""

        verbose_name = 'Categorie'
        verbose_name_plural = 'Categories'

    def __str__(self):
        """Unicode representation of Categorie."""
        return "{}".format(self.titre)

```

## Artist

```python
class Artist(models.Model):
    """Model definition for Artist."""

    # TODO: Define fields here
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    nom_artist = models.CharField(max_length=255)

    class Meta:
        """Meta definition for Artist."""

        verbose_name = 'Artist'
        verbose_name_plural = 'Artists'

    def __str__(self):
        """Unicode representation of Artist."""
        return "{}".format(self.nom_artist)

```

## Son
```python
class Son(models.Model):
    """Model definition for Son."""

    # TODO: Define fields here
    auteur = models.ForeignKey('Artist', related_name='Artist_son', on_delete=models.CASCADE)
    titre = models.CharField(max_length=255)
    categorie = models.ForeignKey('Categorie', related_name='categorie_son', on_delete=models.CASCADE)
    cover = models.ImageField(upload_to='cover_son/')
    fichier =models.FileField(upload_to='Sons/', max_length=100)
    date_add = models.DateTimeField(auto_now_add= True)
    date_upd= models.DateTimeField(auto_now=True)
    statut = models.BooleanField(default=False)

    class Meta:
        """Meta definition for Son."""

        verbose_name = 'Son'
        verbose_name_plural = 'Sons'

    def __str__(self):
        """Unicode representation of Son."""
        return "{} : {}".format(self.auteur, self.titre)

```


## Album
```python
class Album(models.Model):
    """Model definition for Album."""

    # TODO: Define fields here
    auteur = models.ForeignKey(Artist, related_name='artist_albums', on_delete = models.CASCADE)
    titre = models.CharField(max_length=255)
    cover = models.ImageField(upload_to='cover_album/')
    categorie = models.ForeignKey('Categorie', related_name='categorie_son', on_delete=models.CASCADE)
    date_add = models.DateTimeField(auto_now_add= True)
    date_upd= models.DateTimeField(auto_now=True)
    sons = models.ManyToManyField('Son', related_name='son_albums', on_delete = models.CASCADE)
    statut = models.BooleanField(default=False)

    class Meta:
        """Meta definition for Album."""

        verbose_name = 'Album'
        verbose_name_plural = 'Albums'

    def __str__(self):
        """Unicode representation of Album."""
        return "{} : {}".format(self.auteur, self.titre)

```


## Commentaire
```python
class Commentaire(models.Model):
    """Model definition for Commentaire."""

    # TODO: Define fields here
    auteur = models.ForeignKey(User, on_delete=models.CASCADE)
    titre = models.CharField(max_length=255)
    contenu = models.TextField()
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_now=True)
    statut = models.BooleanField(default=False)
    post_id = models.ForeignKey('Post', related_name='Post_Commentaire', on_delete=models.CASCADE)
    statut = models.BooleanField(default=False)

    class Meta:
        """Meta definition for Commentaire."""

        verbose_name = 'commentaire'
        verbose_name_plural = 'commentaires'

    def __str__(self):
        """Unicode representation of Commentaire."""
        return "{} : {}".format(self.auteur, self.titre)

```