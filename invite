import aminofix, concurrent.futures
import os
import pyfiglet
from colored import fore, back, style, attr
attr(0)
print(f"""\u001b[38;5;124m
Script by Capi 

░█████╗░░█████╗░██████╗░██╗███╗░░██╗██╗░░░██╗██╗████████╗███████╗
██╔══██╗██╔══██╗██╔══██╗██║████╗░██║██║░░░██║██║╚══██╔══╝██╔════╝
██║░░╚═╝███████║██████╔╝██║██╔██╗██║╚██╗░██╔╝██║░░░██║░░░█████╗░░
██║░░██╗██╔══██║██╔═══╝░██║██║╚████║░╚████╔╝░██║░░░██║░░░██╔══╝░░
╚█████╔╝██║░░██║██║░░░░░██║██║░╚███║░░╚██╔╝░░██║░░░██║░░░███████╗
░╚════╝░╚═╝░░╚═╝╚═╝░░░░░╚═╝╚═╝░░╚══╝░░░╚═╝░░░╚═╝░░░╚═╝░░░╚══════╝
""")
client = aminofix.Client()
email = input("Email: ")
password = input("Senha: ")
client.login(email=email, password=password)
clients = client.sub_clients(size=100)
for x, name in enumerate(clients.name, 1):
    print(f"{x}.{name}")
communityid = clients.comId[int(input("Selecione a comunidade: "))-1]
SUB = aminofix.SubClient(comId=communityid, profile=client.profile)
chats = SUB.get_chat_threads(size=150)
for z, title in enumerate(chats.title, 1):
	print(f"{z}.{title}")
chatx = chats.chatId[int(input("Selecione o chat: "))-1]


def inviteonlineusers():
	with concurrent.futures.ThreadPoolExecutor(max_workers=10000) as executor:
		for i in range(0, 20000, 250):
			onlineusers = SUB.get_online_users(start=i, size=5000).profile.userId
			if onlineusers:
				for userId in onlineusers:
					print(f"{userId} Enviado/.....")
					_ = [executor.submit(SUB.invite_to_chat, userId,chatx)]
			else:
				break
		for i in range(0, 20000, 250):
			publichats = SUB.get_public_chat_threads(type="recomendado", start=i, size=5000).chatId
			chatsuin = SUB.get_chat_threads(start=i, size=100).chatId
			chats = [*publichats, *chatsuin]
			if chats:
				for chatid in chats:
					for u in range(0, 1000, 50):
						users = SUB.get_chat_users(chatId=chatid, start=u, size=100).userId
						if users:
							for userId in users:
								try:
									print(f"{userId} Enviado/....")
									_ = [executor.submit(SUB.invite_to_chat, userId,chatx)]
								except:
									pass
						else:
							break
							print("Todos os úsuarios Online Convidados")
def inviteuserfollowers():
	userlink=input("Digite o link do usuário: ")
	user=client.get_from_code(userlink)
	userx=user.objectId
	with concurrent.futures.ThreadPoolExecutor(max_workers=10000) as executor:
		for i in range(0, 20000, 250):
			followers = SUB.get_user_followers(userId=userx, start=i, size=100).profile.userId
			if followers:
				for userId in followers:
					try:
						print(f"{userId} Enviado/....")
						_ = [executor.submit(SUB.invite_to_chat, userId, chatx)]
					except:
						pass
			else:
				break
				print("Seguidores de úsuarios Convidados/....")

def inviterecentusers():
	with concurrent.futures.ThreadPoolExecutor(max_workers=10000) as executor:
		for i in range(0, 20000, 250):
			recentusers = SUB.get_all_users(type="recente", start=i, size=100).profile.userId
			users = [*recentusers]
			if users:
				for userId in users:
					print(f"{userId} Enviado/.....")
					_ = [executor.submit(SUB.invite_to_chat, userId, chatx)]
			else:
				break
				print("Usuários recentes e Banidos Convidados")

def inviteallusers():
	with concurrent.futures.ThreadPoolExecutor(max_workers=10000) as executor:
		for i in range(0, 20000, 250):
			onlineusers = SUB.get_online_users(start=i, size=100).profile.userId
			recentusers = SUB.get_all_users(type="recent", start=i, size=100).profile.userId
			curators = SUB.get_all_users(type="curators", start=i, size=100).profile.userId
			leaders = SUB.get_all_users(type="leaders", start=i, size=100).profile.userId
			users = [*onlineusers, *recentusers, *curators, *leaders]
			if users:
				for userId in users:
					print(f"{userId} Enviado/....")
					_ = [executor.submit(SUB.invite_to_chat, userId, chatx)]
			else:
				break
		for i in range(0, 20000, 250):
			publichats = SUB.get_public_chat_threads(type="recomendado", start=i, size=100).chatId
			chatsuin = SUB.get_chat_threads(start=i, size=100).chatId
			chats = [*publichats, *chatsuin]
			if chats:
				for chatid in chats:
					for u in range(0, 1000, 50):
						users = SUB.get_chat_users(chatId=chatid, start=u, size=100).userId
						if users:
							for userId in users:
								try:
									print(f"{userId} Enviado/....")
									_ = [executor.submit(SUB.invite_to_chat, userId, chatx)]
								except:
									pass
						else:
							break
							print("Todos os úsuarios online Convidados:")

print("    1.Convidar úsuarios online:")
print("    2.Convidar seguidores do úsuario:")
print("    3.Convidar úsuarios recentes:")
print("    4.Convidar todos os úsuarios:")
inviteselect = input("Número do tipo: ")
if inviteselect == "1":
	inviteonlineusers()

elif inviteselect == "2":
	inviteuserfollowers()

elif inviteselect == "3":
	inviterecentusers()

elif inviteselect == "4":
	inviteallusers()
