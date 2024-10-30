## 1: Вводим следующие команды:
```
sudo apt update
sudo apt upgrade
```
## 2: Устанавливаем fonts
```
sudo apt-get install figlet
figlet -f /usr/share/figlet/starwars.flf
```
## 3: Устанавливаем бинарник 
```
LATEST_VERSION=$(curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | grep 'tag_name' | cut -d\" -f4)
EXECUTOR_URL="https://github.com/t3rn/executor-release/releases/download/${LATEST_VERSION}/executor-linux-${LATEST_VERSION}.tar.gz"
curl -L -o executor-linux-${LATEST_VERSION}.tar.gz $EXECUTOR_URL
```
## 4: Извлекаем бинарник 
```
tar -xzvf executor-linux-${LATEST_VERSION}.tar.gz
rm -rf executor-linux-${LATEST_VERSION}.tar.gz
cd executor/executor/bin
```
## 5: Устанавливаем screen 
```
screen -S t3rn
```
Если при установке Screen выдаст ошибку, что комнада не найдена, введите следующие комнады
```
sudo apt-get update
sudo apt-get install screen
```
## 6: Устанавливаем среду ноды
```
export NODE_ENV=testnet
```
## 7: Устанавливаем настройки логов
```
export LOG_LEVEL=debug
export LOG_PRETTY=false
export EXECUTOR_PROCESS_ORDERS=true
export EXECUTOR_PROCESS_CLAIMS=true
```
## 8: Устанавливаем переменную, и заменяем приватный ключ от кошелька на приватник того кошелька который будет участвовать в фарме токенов $BRT
```
export PRIVATE_KEY_LOCAL=Приватный_ключ_от_вашего_EVM_кошелька
```
## 9: Указываем сети в которых будем совершать кросс-чейн обмен
```
export ENABLED_NETWORKS='base-sepolia,arbitrum-sepolia,optimism-sepolia,blast-sepolia,l1rn'
```
## 10: Стартуем
```
./executor
```
Выход из screen - Ctrl + A + D
```
