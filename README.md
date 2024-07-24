Para el efecto, se deberá crear un pool de agentes en azure devops:
![image](https://github.com/user-attachments/assets/df6d097f-9688-45f4-8e1c-44db23a8b4a6)

El nombre será utilizado dentro del yaml secret que se ejecutará en minishift. También se deberá crear en azure devops un personal access token:
![image](https://github.com/user-attachments/assets/8a783d4f-13b3-4db7-a7b6-1f0ed0c91632)

Todos los datos se deberan convertir a base 64 para agregarlos al secret, ejemplo:
$echo -n 'axjhgheijnom5tuliujnuzbqobvy5dnalgdzqj7v3kpmhxyxefgq' | base64
$YXhqaGdoZWlqbm9tNXR1bGl1am51emJxb2J2eTVkbmFsZ2R6cWo3djNrcG1oeHl4ZWZncQ==

Quedando el secret de la siguiente forma:
apiVersion: v1
data:
  AZP_POOL: T3BlbnNoaWZ0LUFnZW50 #Openshift-Agent
  #AZP_KEY: axjhgheijnom5tuliujnuzbqobvy5dnalgdzqj7v3kpmhxyxefgq
  AZP_TOKEN: YXhqaGdoZWlqbm9tNXR1bGl1am51emJxb2J2eTVkbmFsZ2R6cWo3djNrcG1oeHl4ZWZncQ== #axjhgheijnom5tuliujnuzbqobvy5dnalgdzqj7v3kpmhxyxefgq
  AZP_URL: aHR0cHM6Ly9kZXYuYXp1cmUuY29tL2FsZXhwb3J0aWxsbzg4Lw== #https://dev.azure.com/alexportillo88/
kind: Secret
metadata:
  name: azdevops
  namespace: az-devops
type: Opaque
