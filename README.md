# Español
# acción fail2ban xmpp
Una acción que te permite enviar mensajes xmpp.
# Uso
## Prerrequisitos

El trabajo de envío se delega a `sendxmpp`.

Instalación en debian:

    $ sudo apt-get install sendxmpp 

## Preparación

`sendxmpp` necesita un archivo de configuración que contenga la información de la cuenta del remitente:

    fail2ban@mi-servidor-xmpp mi-super-clave-secreta 

No olvides proteger el archivo después de la creación:

    $ chmod 600 .sendxmpprc 

## Instalación en fail2ban

Simplemente copie el archivo de acción en su carpeta actions.d :

    $ sudo cp xmpp.conf /etc/fail2ban/actions.d 

## Configuración

Aquí hay una configuración de ejemplo en el jail.local :

    [DEFECTO]
    destxmpp = quien-recibe@mi-servidor
    xmpprcfile = /ruta-completa-al-archivo-de-configuracion/.sendxmpprc
    
    [sshd]
    puerto = ssh
    logpath =% (sshd_log) s
    action = xmpp [ destxmpp = " % (destxmpp) s " , rcfile = " % (xmpprcfile) s " , nombre =% (__ name __) s, bantime = " % (bantime) s " ] 

Es necesario definir dos valores:

`destxmpp` : esta es la cuenta xmpp de receving
`xmpprcfile` : la ruta al archivo de recursos sendxmpp preparado 


# English

# fail2ban xmpp action

An action that lets you send xmpp messages.

# Usage

## Prerequisites

The actual send job is delegated to `sendxmpp`.

Installation on debian:

    # apt install sendxmpp

## Preparation

`sendxmpp` itself needs a resource file which holds the account information of the sender:

    fail2ban@my-xmpp-server.net my-secret-password

Don't forget to protect the file after creation:

    # chmod 600 .sendxmpprc

## Installation

Just copy the action file into your `actions.d` folder:

    # cp xmpp.conf /etc/fail2ban/actions.d

## Configuration

Here is an example configuration in the `jail.local`:

```ini
[DEFAULT]
destxmpp = your-account@jabber.de
xmpprcfile = /root/.sendxmpprc

[sshd]
port    = ssh
logpath = %(sshd_log)s
action  = xmpp[destxmpp="%(destxmpp)s", rcfile="%(xmpprcfile)s", name=%(__name__)s, bantime="%(bantime)s"]
```

You need to define two values:

- `destxmpp`: this is the receving xmpp account
- `xmpprcfile`: the path to your prepared sendxmpp resource file
