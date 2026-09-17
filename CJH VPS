#!/bin/bash

# Clear terminal for clean dashboard view
clear

# ==========================================
# 🌟 INFINITE LABS COLOR CODES & FX
# ==========================================
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
PURPLE='\033[0;35m'
CYAN='\033[0;36m'
WHITE='\033[1;37m'
NC='\033[0m'

# ==========================================
# FUNCTION: TYPING EFFECT ANIMATION
# ==========================================
type_effect() {
    local text="$1"
    local delay="$2"

    for (( i=0; i<${#text}; i++ )); do
        echo -n "${text:$i:1}"
        sleep "$delay"
    done

    echo ""
}

# ==========================================
# FUNCTION: LOADING BAR ANIMATION
# ==========================================
loading_bar() {
    local title="$1"

    echo -ne "${YELLOW}⏳ $title ${NC}[          ]"
    sleep 0.3
    echo -ne "\b\b\b\b\b\b\b\b\b\b\b[===       ]"
    sleep 0.3
    echo -ne "\b\b\b\b\b\b\b\b\b\b\b[======    ]"
    sleep 0.3
    echo -ne "\b\b\b\b\b\b\b\b\b\b\b[========= ]"
    sleep 0.3
    echo -ne "\b\b\b\b\b\b\b\b\b\b\b[==========]"

    echo -e " ${GREEN}DONE!${NC}"
}

# ==========================================
# AUTOMATED ROOT/SUDO PRIVILEGE CHECK
# ==========================================
if [ "$(id -u)" -eq 0 ]; then
    SUDO_CMD=""
else
    SUDO_CMD="sudo"
fi

# ==========================================
# MAIN INTERACTIVE DASHBOARD
# ==========================================
show_menu() {
    clear

    echo ""
    echo -e "${BLUE}                         INFINITE LABS${NC}"
    echo -e "${BLUE}                    ─────────────────────${NC}"
    echo -e "${WHITE}                      VPS CONTROL PANEL${NC}"
    echo ""

    echo -e "${BLUE}     ┌──────────────────────────────────────────────────┐${NC}"
    echo -e "${BLUE}     │  ${WHITE}SYSTEM${BLUE}                                          │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"
    echo -e "${BLUE}     │  ${GREEN}● ONLINE${BLUE}        ${CYAN}QEMU/KVM${BLUE}        ${YELLOW}TCP NETWORK${BLUE}     │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"
    echo -e "${BLUE}     └──────────────────────────────────────────────────┘${NC}"
    echo ""

    echo -e "${BLUE}     ┌─────────────────── ${WHITE}MAIN MENU${BLUE} ─────────────────────┐${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"

    echo -e "${BLUE}     │   ${CYAN}01${BLUE}  ›  ${WHITE}CREATE VPS${BLUE}                              │${NC}"
    echo -e "${BLUE}     │       ${WHITE}Deploy a new Ubuntu virtual machine${BLUE}        │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"

    echo -e "${BLUE}     │   ${CYAN}02${BLUE}  ›  ${WHITE}RESTART VPS${BLUE}                             │${NC}"
    echo -e "${BLUE}     │       ${WHITE}Start existing VPS instance${BLUE}                │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"

    echo -e "${BLUE}     │   ${CYAN}03${BLUE}  ›  ${WHITE}NETWORK${BLUE}                                 │${NC}"
    echo -e "${BLUE}     │       ${WHITE}Configure TCP port forwarding${BLUE}              │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"

    echo -e "${BLUE}     │   ${CYAN}04${BLUE}  ›  ${WHITE}CLEANUP${BLUE}                                 │${NC}"
    echo -e "${BLUE}     │       ${WHITE}Remove VPS files and cache${BLUE}                 │${NC}"
    echo -e "${BLUE}     │                                                  │${NC}"

    echo -e "${BLUE}     │   ${CYAN}05${BLUE}  ›  ${WHITE}EXIT${BLUE}                                    │${NC}"
    echo -e "${BLUE}     │       ${WHITE}Close control panel${BLUE}                        │${NC}"

    echo -e "${BLUE}     │                                                  │${NC}"
    echo -e "${BLUE}     └──────────────────────────────────────────────────┘${NC}"
    echo ""

    echo -e "${BLUE}     ─────────────────────────────────────────────────────${NC}"
    echo -e "${WHITE}       INFINITE LABS  •  VPS MANAGER  •  ${GREEN}READY${WHITE}${NC}"
    echo -e "${BLUE}     ─────────────────────────────────────────────────────${NC}"
    echo ""

    echo -ne "${CYAN}     Select option › [1-5]: ${NC}"
    read CHOICE

    case $CHOICE in
        1)
            create_vps
            ;;
        2)
            restart_vps
            ;;
        3)
            configure_tcp
            ;;
        4)
            clean_vps
            ;;
        5)
            clear
            echo ""
            echo -e "${BLUE}     INFINITE LABS VPS Manager closed.${NC}"
            echo ""
            exit 0
            ;;
        *)
            echo ""
            echo -e "${RED}     ❌ Invalid choice! Please select 1-5.${NC}"
            sleep 2
            show_menu
            ;;
    esac
}

# ==========================================
# STEP 1: CONFIGURE STORAGE & DOWNLOAD CLOUD IMAGE
# ==========================================
create_vps() {
    clear

    echo ""
    echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
    echo -e "${BLUE}     ║              ${WHITE}CREATE NEW VPS${BLUE}                  ║${NC}"
    echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"
    echo ""

    echo -ne "${CYAN}     🔹 Enter RAM Size in GB (e.g., 4, 8, 16, 32): ${NC}"
    read RAM_GB

    echo -ne "${CYAN}     🔹 Enter CPU Cores (e.g., 2, 4, 8): ${NC}"
    read CPU_CORES

    echo -ne "${CYAN}     🔹 Enter Disk Space to ADD in GB (e.g., 10, 20): ${NC}"
    read DISK_ADD

    echo -ne "${CYAN}     🔹 Create Username (Default: ubuntu): ${NC}"
    read USER_NAME

    USER_NAME=${USER_NAME:-ubuntu}

    echo -ne "${CYAN}     🔹 Create Password (Default: 1234): ${NC}"
    read USER_PASS

    USER_PASS=${USER_PASS:-1234}

    TCP_HOST_PORT=${TCP_HOST_PORT:-2222}
    TCP_GUEST_PORT=22

    echo ""
    echo -e "${YELLOW}     ⏳ Installing core dependencies... Please wait.${NC}"
    echo ""

    $SUDO_CMD apt-get update -y > /dev/null 2>&1

    $SUDO_CMD apt-get install -y \
        qemu-system-x86 \
        qemu-utils \
        wget \
        cloud-image-utils \
        curl \
        lsof > /dev/null 2>&1

    # Custom absolute path architecture build
    $SUDO_CMD mkdir -p /home/CJH > /dev/null 2>&1

    # Download Ubuntu 22.04 cloud image
    if [ ! -f "/home/CJH/ubuntu22.qcow2" ]; then

        echo -e "${YELLOW}     📥 Downloading Ubuntu 22.04 Cloud Image...${NC}"

        $SUDO_CMD wget -q --show-progress \
            https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img \
            -O /home/CJH/ubuntu22.qcow2

        $SUDO_CMD chmod 666 /home/CJH/ubuntu22.qcow2

    else

        echo -e "${GREEN}     ✅ Existing Ubuntu Image Cache Detected.${NC}"

    fi

    loading_bar "Generating Cloud-Init Matrix"

    cat <<EOF > user-data
#cloud-config
ssh_pwauth: True
chpasswd:
  list: |
    ${USER_NAME}:${USER_PASS}
  expire: False
EOF

    cloud-localds seed.img user-data > /dev/null 2>&1

    loading_bar "Expanding Server Hard Disk Allocation"

    $SUDO_CMD qemu-img resize \
        /home/CJH/ubuntu22.qcow2 \
        +${DISK_ADD}G > /dev/null 2>&1

    save_env
    boot_qemu
}

# ==========================================
# STEP 2: NETWORK CONTROL MODIFIER
# ==========================================
configure_tcp() {
    clear

    echo ""
    echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
    echo -e "${BLUE}     ║             ${WHITE}NETWORK CONFIGURATION${BLUE}             ║${NC}"
    echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"
    echo ""

    if [ -f ".vps_env" ]; then
        source .vps_env
    fi

    echo -e "     Current Target Host Port  : ${CYAN}${TCP_HOST_PORT:-2222}${NC}"
    echo -e "     Current Guest VM Port     : ${CYAN}${TCP_GUEST_PORT:-22}${NC}"
    echo ""

    echo -ne "${CYAN}     🔹 Enter NEW External Host Port (Default: 2222): ${NC}"
    read NEW_HOST_PORT

    TCP_HOST_PORT=${NEW_HOST_PORT:-2222}

    echo -ne "${CYAN}     🔹 Enter Internal Guest Port (Default SSH: 22): ${NC}"
    read NEW_GUEST_PORT

    TCP_GUEST_PORT=${NEW_GUEST_PORT:-22}

    save_env

    echo ""
    echo -e "${GREEN}     ✅ TCP Rule Updated Successfully!${NC}"

    sleep 2
    show_menu
}

# ==========================================
# SAVE VPS ENVIRONMENT
# ==========================================
save_env() {

    echo "RAM_GB=${RAM_GB:-32}" > .vps_env
    echo "CPU_CORES=${CPU_CORES:-4}" >> .vps_env
    echo "USER_NAME=${USER_NAME:-ubuntu}" >> .vps_env
    echo "USER_PASS=${USER_PASS:-1234}" >> .vps_env
    echo "TCP_HOST_PORT=${TCP_HOST_PORT:-2222}" >> .vps_env
    echo "TCP_GUEST_PORT=${TCP_GUEST_PORT:-22}" >> .vps_env
}

# ==========================================
# STEP 3: START VPS & SSHX ACCESS
# ==========================================
boot_qemu() {

    if [ -f ".vps_env" ]; then
        source .vps_env
    fi

    TCP_HOST_PORT=${TCP_HOST_PORT:-2222}
    TCP_GUEST_PORT=${TCP_GUEST_PORT:-22}

    RAM_VALUE="${RAM_GB:-32}G"

    clear

    echo ""
    echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"

    type_effect \
        "     🚀 INFINITE LABS SYSTEM SYNCHRONIZED! STARTING VM..." \
        0.02

    echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"
    echo ""

    # Start SSHX tunnel
    sshx_log=$(mktemp)

    curl -sSf https://sshx.io/get | sh -s run \
        > "$sshx_log" 2>&1 &

    sleep 5

    SSHX_URL=$(grep -o \
        'https://sshx.io/s/[a-zA-Z0-9]*' \
        "$sshx_log" | head -n 1)

    rm -f "$sshx_log"

    clear

    echo ""
    echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
    echo -e "${BLUE}     ║              ${GREEN}✓ VM NETWORK ACTIVE${BLUE}                ║${NC}"
    echo -e "${BLUE}     ╠══════════════════════════════════════════════════╣${NC}"
    echo -e "${BLUE}     ║ ${WHITE}👤 Username : ${CYAN}${USER_NAME:-ubuntu}${BLUE}                         ║${NC}"
    echo -e "${BLUE}     ║ ${WHITE}🔑 Password : ${CYAN}${USER_PASS:-1234}${BLUE}                           ║${NC}"
    echo -e "${BLUE}     ║ ${WHITE}⚙️  Resources: ${CYAN}${RAM_VALUE} RAM | ${CPU_CORES:-4} Cores${BLUE}       ║${NC}"
    echo -e "${BLUE}     ║ ${WHITE}🚀 Port Rule : ${YELLOW}${TCP_HOST_PORT} → ${TCP_GUEST_PORT}${BLUE}                  ║${NC}"
    echo -e "${BLUE}     ╠══════════════════════════════════════════════════╣${NC}"

    if [ ! -z "$SSHX_URL" ]; then

        echo -e "${BLUE}     ║ ${YELLOW}🔥 LIVE SSHX ACCESS LINK:${BLUE}                         ║${NC}"
        echo -e "${BLUE}     ║ ${GREEN}$SSHX_URL${BLUE}                                      ║${NC}"

    else

        echo -e "${BLUE}     ║ ${RED}⚠️ SSHX tunnel loading slow.${BLUE}                      ║${NC}"
        echo -e "${BLUE}     ║ ${WHITE}Direct local network port is listening.${BLUE}         ║${NC}"

    fi

    echo -e "${BLUE}     ╠══════════════════════════════════════════════════╣${NC}"
    echo -e "${BLUE}     ║ ${WHITE}👉 Connection Command:${BLUE}                           ║${NC}"
    echo -e "${BLUE}     ║ ${CYAN}ssh ${USER_NAME:-ubuntu}@localhost -p ${TCP_HOST_PORT}${BLUE}             ║${NC}"
    echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"
    echo ""

    # ==========================================
    # QEMU VM EXECUTION
    # ==========================================

    qemu-system-x86_64 \
        -hda /home/CJH/ubuntu22.qcow2 \
        -m $RAM_VALUE \
        -smp ${CPU_CORES:-4} \
        -drive file=seed.img,format=raw \
        -nographic \
        -netdev user,id=net0,hostfwd=tcp::${TCP_HOST_PORT}-:${TCP_GUEST_PORT} \
        -device e1000,netdev=net0
}

# ==========================================
# RESTART PIPELINE
# ==========================================
restart_vps() {

    clear

    if [ -f "/home/CJH/ubuntu22.qcow2" ] && [ -f "seed.img" ]; then

        echo ""
        echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
        echo -e "${BLUE}     ║        ${GREEN}🔄 RESTARTING INFINITE LABS VPS${BLUE}          ║${NC}"
        echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"

        sleep 1

        boot_qemu

    else

        echo ""
        echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
        echo -e "${BLUE}     ║ ${RED}❌ No active VPS configuration found.${BLUE}            ║${NC}"
        echo -e "${BLUE}     ║ ${WHITE}Build the VPS using Option 1.${BLUE}                    ║${NC}"
        echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"

        sleep 3

        show_menu
    fi
}

# ==========================================
# CLEAN PIPELINE
# ==========================================
clean_vps() {

    clear

    echo ""
    echo -e "${BLUE}     ╔══════════════════════════════════════════════════╗${NC}"
    echo -e "${BLUE}     ║              ${YELLOW}⚠ CLEAN WORKSPACE${BLUE}                 ║${NC}"
    echo -e "${BLUE}     ╚══════════════════════════════════════════════════╝${NC}"
    echo ""

    echo -e "${YELLOW}     ⚠️ Purging VPS storage components and configurations...${NC}"

    $SUDO_CMD rm -rf \
        user-data \
        seed.img \
        /home/CJH/ubuntu22.qcow2 \
        .vps_env

    pkill sshx > /dev/null 2>&1
    pkill sh > /dev/null 2>&1

    sleep 1

    echo -e "${GREEN}     ✅ INFINITE LABS workspace successfully cleaned!${NC}"

    sleep 2

    show_menu
}

# ==========================================
# EXECUTE DASHBOARD
# ==========================================
show_menu
