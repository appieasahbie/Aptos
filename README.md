# Full node installation on Aptos



<img width="1200" alt="aptos_meta_og_aptos-labs-5e53cba6bf9a1a30e03301fd6ff233a4b7c123de" src="https://user-images.githubusercontent.com/108979536/207708751-cec713da-a128-4b9f-8801-871d455d7787.png">



Committed to developing products and applications on the Aptos blockchain that redefine the web3 user experience.



# 1 : First Install dependencies:

      sudo apt-get install jq unzip -y


  ### Install Screen
  
     sudo apt install screen -y
 
  ### Install git
  
     apt install git -y

  ### Install cargo
  
     apt install cargo -y
     
     
# 2 :  Clone the Aptos Repo

     git clone https://github.com/aptos-labs/aptos-core.git
     
 
  ### Switch to aptos-core
  
     cd aptos-core

  ### Prepare your developer environment
     
     ./scripts/dev_setup.sh -y
     
     
  ### Update the current shell environment   
     
      source ~/.cargo/env


# 3 : Setup the Full Node
     
     
   ### Checkout the testnet

       git checkout --track origin/devnet
 
   ### create a copy of the fullnode config template
   
        cp config/src/config/test_data/public_full_node.yaml fullnode.yaml

  
 # 4 : Download genesis.blob
 
        curl -O https://devnet.aptoslabs.com/genesis.blob

   ### Download Waypoint.txt

        curl -O https://devnet.aptoslabs.com/waypoint.txt

   ### Open your config file

        sudo nano /root/aptos-core/fullnode.yaml
   
   ( modify the config: Remplace 127.0.0.1 by 0.0.0.0 by listen address and api-address enter ctrl + x then y enter)
   
   
  # 5 : Open ports (Switch to home )
  
       cd $home
       
  And
  
       apt install ufw -y 
       ufw allow ssh 
       ufw allow https 
       ufw allow http 
       ufw allow 6180
       ufw allow 6182 
       ufw allow 80 
       ufw allow 9101 
       ufw allow 181 
       ufw allow 182 
       ufw allow 8080 
       ufw allow 9103 
       ufw enable
       
       
# 6 : Aptos CLi
 
      cd aptos-core
      
  ### Install Aptos cli 2.6

      cargo install --git https://github.com/aptos-labs/aptos-core.git aptos --branch devnet
      
      
# 7 : Generate Keys

      aptos key generate --key-type x25519 --output-file /root/aptos-core/private-key.txt


  ### Genere peers:

      aptos key extract-peer  --private-key-file private-key.txt  \
    --output-file peer-info.yaml
    
  ### Copy your public key full node
  
      sudo nano peer-info.yaml
      
      
# 8 : Launch the  Fullnode

      cd aptos-core
 
  ### Create a screen session called “aptos-core”
  
      screen -S aptos-core

  ### Run the full node
  
  
      cargo run -p aptos-node --release -- -f ~/aptos-core/fullnode.yaml

 
 

[buy me a cup of coffee](https://www.paypal.com/paypalme/AbdelAkridi?country.x=NL&locale.x=en_US)     
     
     
     
     
     
     
     

     
