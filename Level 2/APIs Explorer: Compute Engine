export ZONE=$(gcloud compute project-info describe \
--format="value(commonInstanceMetadata.items[google-compute-default-zone])") 

gcloud services enable compute.googleapis.com

sleep 20


curl -X POST "https://compute.googleapis.com/compute/v1/projects/$DEVSHELL_PROJECT_ID/zones/$ZONE/instances" \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  -d "{
    \"name\": \"instance-1\",
    \"machineType\": \"zones/$ZONE/machineTypes/n1-standard-1\",
    \"networkInterfaces\": [{}],
    \"disks\": [{
      \"type\": \"PERSISTENT\",
      \"boot\": true,
      \"initializeParams\": {
        \"sourceImage\": \"projects/debian-cloud/global/images/family/debian-11\"
      }
    }]
  }"

function check_progress {
    while true; do
        echo
        echo -n "${BOLD}${YELLOW}check your progress for task 2 before proceeding further, then type Y and hit Enter ? (Y/N): ${RESET}"
        read -r user_input
        if [[ "$user_input" == "Y" || "$user_input" == "y" ]]; then
            echo
            echo "${BOLD}${GREEN}ok now go back and check rest of progress${RESET}"
            echo
            break
        elif [[ "$user_input" == "N" || "$user_input" == "n" ]]; then
            echo
            echo "${BOLD}${RED}cant proceed further${RESET}"
        else
            echo
            echo "${BOLD}${MAGENTA}Invalid input. Please enter Y or N.${RESET}"
        fi
    done
}


check_progress


curl -X DELETE \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://compute.googleapis.com/compute/v1/projects/$DEVSHELL_PROJECT_ID/zones/$ZONE/instances/instance-1"



echo -e "\n" 

cd

remove_files() {
    # Loop through all files in the current directory
    for file in *; do
        # Check if the file name starts with "gsp", "arc", or "shell"
        if [[ "$file" == gsp* || "$file" == arc* || "$file" == shell* ]]; then
            # Check if it's a regular file (not a directory)
            if [[ -f "$file" ]]; then
                # Remove the file and echo the file name
                rm "$file"
                echo "File removed: $file"
            fi
        fi
    done
}

remove_files
