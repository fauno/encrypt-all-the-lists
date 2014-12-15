# Listas de correo cifradas

O llaves privadas compartidas, basado en experimentos vistos en
hacktivistas@listas.sindominio.net :)

Se trata de crear una llave privada para una identidad común (como una
lista de correo), que luego se comparte entre todas las participantes.

Esto permite tener una conversación cifrada de una a muchas sin
desarrollo extra, sólo considera a las destinatarias como una sola
entidad, es decir un conjunto con la misma llave.

## Problemas

* Si alguien se va del grupo hay que renovar las llaves (!)

* No funciona (todavía) con GnuPG 2.1, por [esta
  regresión](http://lists.gnupg.org/pipermail/gnupg-devel/2014-October/028919.html)
  que también afecta a [monkeysphere](https://monkeysphere.info)

## Ventajas

* No hay que implementar software nuevo

* El servidor de listas no sabe nada sobre el contenido de los mensajes
  ([otras implementaciones descifran y vuelven a cifrar](https://schleuder2.nadir.org/))

## Uso

Crear una llave para una lista:

    crear-lista-cifrada hacktivistas@listas.sindominio.net participante1 participante2...

Devuelve un archivo `hacktivistas@listas.sindominio.net.asc` cifrado
para todas las participantes especificadas.

Importar la llave localmente:

    importar-lista-cifrada hacktivistas@listas.sindominio.net.asc

Esto hace dos cosas:

* Importa la llave pública de la lista, para que podamos cifrar mensajes
  destinados a esta

* Importa la llave privada de la lista, para que podamos descifrar los
  mensajes enviados

Ver las llaves:

    gpg --list-secret-keys

Invitar a alguien más:

    exportar-lista-cifrada hacktivistas@listas.sindominio.net fauno@endefensadelsl.org

## Referencias

* [OpenPGP Best Practices](https://we.riseup.net/riseuplabs+paow/openpgp-best-practices)
* [Moving a GPG Key (Privately)](http://montemazuma.wordpress.com/2010/03/01/moving-a-gpg-key-privately/)
* [Creating the perfect GPG keypair](https://alexcabal.com/creating-the-perfect-gpg-keypair/)
