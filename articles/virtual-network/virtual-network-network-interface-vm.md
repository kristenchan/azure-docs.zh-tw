---
title: "在 Azure 虛擬機器中新增或移除網路介面 | Microsoft Docs"
description: "了解如何在虛擬機器中新增網路介面或移除網路介面。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: 7df1dfbea8c985907d5330819dc1e7bf1578aafa
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2017
---
# <a name="add-network-interfaces-to-or-remove-from-virtual-machines"></a>在虛擬機器中新增或移除網路介面

了解如何在建立 VM 時新增現有的網路介面，或在處於已停止 (已取消配置) 狀態的現有 VM 中新增或移除網路介面。 網路介面可讓 Azure 虛擬機器 (VM) 與網際網路、Azure 以及內部部署資源進行通訊。 一個 VM 可以有一或多個網路介面。 

如果您需要新增、變更或移除網路介面的 IP 位址，請閱讀[管理網路介面 IP 位址](virtual-network-network-interface-addresses.md)一文。 如果您需要建立、變更或刪除網路介面，請閱讀[管理網路介面](virtual-network-network-interface.md)一文。

## <a name="before"></a>開始之前

在完成本文任一節的任何步驟之前，請先完成下列工作︰

- 檢閱 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的文章，以了解每個 Linux 和 Windows VM 大小所支援的網路介面數目。
- 使用 Azure 帳戶來登入 Azure [入口網站](https://portal.azure.com)、Azure 命令列介面 (CLI) 或 Azure PowerShell。 如果您還沒有 Azure 帳戶，請註冊[免費試用帳戶](https://azure.microsoft.com/free)。
- 如果您使用 PowerShell 命令來完成本文中的工作，請[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json)。 請確定您已安裝最新版的 Azure PowerShell commandlet。 若要取得 PowerShell 命令的說明 (包含範例)，請輸入 `get-help <command> -full`。
- 如果您使用 Azure 命令列介面 (CLI) 命令來完成本文中的工作，請[安裝和設定 Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。 請確定您已安裝最新版的 Azure CLI。 若要取得 CLI 命令的說明，請輸入 `az <command> --help`。 您可以不安裝 CLI 及其必要條件，而是改用 Azure Cloud Shell。 Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。 它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。 若要使用 Cloud Shell，請按一下[入口網站](https://portal.azure.com)頂端的 Cloud Shell (**> _**) 按鈕。

## <a name="about"></a>關於網路介面和 VM

您可以在建立 VM 時將現有的網路介面新增 (連接) 至該 VM，但前提是該網路介面目前並未連接至其他 VM。 您可以在現有 VM 中新增網路介面或從中移除 (中斷連接) 網路介面，前提是該 VM 處於已停止 (已取消配置) 狀態。 如果您使用 Azure 入口網站來建立 VM，入口網站就會以預設設定為您建立網路介面。 入口網站無法讓您︰

- 在建立 VM 時指定要新增的現有網路介面
- 建立具有多個網路介面的 VM
- 指定網路介面的名稱 (入口網站會建立具預設名稱的網路介面)

您可以使用 Azure PowerShell 或 CLI，以無法使用於入口網站的所有先前屬性建立網路介面或 VM。 在完成下列各節中的工作之前，請考量下列條件約束和行為︰

- 所有 VM 大小至少都會支援兩個網路介面，但某些 VM 大小可支援兩個以上的網路介面。 在過去，某些 VM 大小僅支援一個網路介面。 若要了解每個 VM 大小所支援的網路介面數目，請閱讀 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的文章。 
- 在過去，網路介面僅可新增至支援多個網路介面且至少以兩個網路介面建立的 VM。 您無法將網路介面新增至使用一個網路介面建立的 VM，即使該 VM 大小支援多個網路介面也一樣。 相反地，由於以至少兩個網路介面所建立的 VM 一定要有至少兩個網路介面，因此您只能從至少具有三個網路介面的 VM 中移除網路介面。 以上這些限制已不再適用。 您現在能夠以任何數目的網路介面建立 VM (最多可達 VM 大小所支援的數目)，以及新增或移除任何數目的網路介面 (從處於已停止 (已取消配置) 狀態的 VM)，只要 VM 一律至少具有一個網路介面即可。
- 根據預設，會將 VM 中的第一個網路介面定義為「主要」網路介面。 VM 中的所有其他網路介面均為「次要」網路介面。
- Azure DHCP 伺服器會對主要網路介面指派預設閘道，但不會對次要網路介面加以指派。 由於系統未對次要網路介面指派預設閘道，因此根據預設，它們無法與其子網路外的資源進行通訊。 若要讓次要網路介面與其子網路之外的資源通訊，請參閱[在具有多個網路介面的虛擬機器作業系統內路由](#routing-within-a-virtual-machine-operating-system-with-multiple-network-interfaces)。
- 根據預設，來自 VM 的所有輸出流量都會送出指派給主要網路介面之主要 IP 組態的 IP 位址。 您可以控制要對 VM 作業系統內的輸出流量使用哪個 IP 位址，但根據預設，流量會透過主要網路介面傳輸。
- 在過去，相同可用性設定組中的所有 VM 都必須具有單一或多個網路介面。 具有任意多個 (最多可達 VM 大小所支援的數目) 網路介面的 VM 現在可存在於相同的可用性設定組中。 然而，只有在建立 VM 時，才能將 VM 新增到可用性設定組。 若要深入了解可用性設定組，請閱讀[在 Azure 中管理 VM 的可用性](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy)一文。
- 雖然相同 VM 中的網路介面可以連線至 VNet 中不同的子網路，但這些網路介面全都必須連線至相同的 VNet。
- 您可以將任何主要或次要網路介面之任何 IP 組態的任何 IP 位址新增至 Azure Load Balancer 後端集區。 在過去，只能將主要網路介面的主要 IP 位址新增到後端集區。 若要深入了解 IP 位址和組態，請閱讀[新增、變更或移除 IP 位址](virtual-network-network-interface-addresses.md)一文。
- 刪除 VM 並不會刪除與其連接的網路介面。 刪除 VM 時，會中斷網路介面與該 VM 的連接。 您可以將網路介面新增至其他 VM，也可以刪除它們。
- 如果為網路介面指派私人 IPv6 位址，您可以在建立 VM 時將該網路介面連接到 VM。 在 VM 建立後，就無法將具有 IPv6 位址的網路介面連接至 VM。 如果您在建立虛擬機器時連接具有私人 IPv6 位址的網路介面，則不論該虛擬機器大小支援多少個網路介面，您只能將該網路介面連接到該 VM。 請參閱[網路介面 IP 位址](virtual-network-network-interface-addresses.md)，進一步瞭解指派 IP 位址給網路介面。

## <a name="vm-create"></a>將現有的網路介面新增至新的 VM

當您透過入口網站建立 VM 時，入口網站會以預設設定為您建立網路介面，並將其連接至該 VM。 您無法將現有的網路介面新增至新的 VM，或使用 Azure 入口網站建立具有多個網路介面的 VM。 這兩項作業都可使用 CLI 或 PowerShell 來進行。 您所建立的 VM 大小能支援多少個網路介面，您在 VM 中就能新增這個數目的網路介面。 若要深入了解每個 VM 大小所支援的網路介面數目，請閱讀 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的文章。 您在某個 VM 中新增的網路介面目前無法連接至另一個 VM。 若要深入了解如何建立網路介面，請閱讀[管理網路介面](virtual-network-network-interface.md#create-a-network-interface)一文。

### <a name="routing-within-a-virtual-machine-operating-system-with-multiple-network-interfaces"></a>在具有多個網路介面的虛擬機器作業系統內路由

Azure 將預設閘道指派給連接至虛擬機器的第一個 (主要) 網路介面。 Azure 不會將預設閘道指派給連接至虛擬機器的其他 (次要) 網路介面。 因此依預設，您無法與次要網路介面中子網路之外的資源進行通訊。 不過，次要網路介面可與其子網路進行通訊，但不同的作業系統有不同的通訊啟用步驟。

### <a name="windows"></a>Windows

從 Windows 命令提示字元完成下列步驟：

1. 執行 `route print` 命令，針對有兩個連接之網路介面的虛擬機器傳回下列的類似輸出：

    ```
    ===========================================================================
    Interface List
    3...00 0d 3a 10 92 ce ......Microsoft Hyper-V Network Adapter #3
    7...00 0d 3a 10 9b 2a ......Microsoft Hyper-V Network Adapter #4
    ===========================================================================
    ```
 
    在此範例中，**Microsoft Hyper-V Network Adapter #4** (介面 7) 是未被指派預設閘道的次要網路介面。

2. 從命令提示字元中執行 `ipconfig` 命令，查看將哪些 IP 位址指派給次要網路介面。 在此範例中，192.168.2.4 會指派給介面 7。 不會為次要網路介面傳回預設閘道位址。

3. 若要將次要網路介面之子網路的外部位址之所有流量路由至子網路的閘道，請執行下列命令：

    ```
    route add -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5015 IF 7
    ```

    子網路的閘道位址是為子網路定義的位址範圍 (以.1 結尾) 的第一個 IP 位址。 如果您不想要路由子網路外部的所有流量，您可以改為將個別的路由新增至特定的目的地。 例如，如果您只想將從次要網路介面的流量路由到 192.168.3.0 網路，請輸入命令：

      ```
      route add -p 192.168.3.0 MASK 255.255.255.0 192.168.2.1 METRIC 5015 IF 7
      ```
  
4. 例如，若要確認與 192.168.3.0 網路上的資源成功通訊，請使用介面 7 (192.168.2.4)，輸入下列命令來 ping 192.168.3.4：

    ```
    ping 192.168.3.4 -S 192.168.2.4
    ```

    您可能需要開啟 ICMP，方法是通過正在使用下列命令來 ping 之裝置的 Windows 防火牆：
  
      ```
      netsh advfirewall firewall add rule name=Allow-ping protocol=icmpv4 dir=in action=allow
      ```
  
5. 若要確認已在路由表中新增路由，請輸入 `route print` 命令，它會傳回類似下列文字的輸出：

    ```
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4     15
              0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.4   5015
    ```

    **閘道**下使用 *192.168.1.1* 列出的路由，是根據主要網路介面預設會在該處的路由。 **閘道**下包含 *192.168.2.1* 的路由是您新增的路由。

### <a name="linux"></a>Linux

由於預設行為會使用弱式主機路由，因此建議您限制相同子網路中資源之間的次要網路介面流量。 如果您需要在次要網路介面的子網路外通訊，您必須建立路由規則，允許虛擬機器透過特定的網路介面來傳送和接收流量。 否則，已定義的預設路由便無法正確處理屬於 eth1 的流量。 若要了解如何設定路由規則，請參閱[設定多個 NIC 的 Linux](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-guest-os-for-multiple-nics)。

> [!WARNING]
> 如果網路介面具有已指派的私人 IPv6 位址，只有在建立虛擬機器時，才能將該網路介面新增至虛擬機器。 只要將 IPv6 位址指派給連結至虛擬機器的網路介面，則無論是建立虛擬機器時或虛擬機器建立後，都不能再將一個以上的網路介面連結到虛擬機器。 請參閱[網路介面 IP 位址](virtual-network-network-interface-addresses.md)，進一步瞭解指派 IP 位址給網路介面。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>將現有的網路介面新增至現有的 VM

您要在其中新增網路介面的 VM 大小能支援多少個網路介面，您在 VM 中就能新增這個數目的網路介面。 若要了解每個 VM 大小所支援的網路介面數目，請閱讀 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 或 [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的文章。 您要在其中新增網路介面的 VM 必須支援想新增的網路介面數量，且必須處於已停止 (已解除配置) 狀態。 您想要新增的網路介面目前無法連接至另一個 VM。 您無法使用 Azure 入口網站，將網路介面新增至現有的 VM。 若要在現有的 VM 新增網路介面，您必須使用 CLI 或 PowerShell。 

Azure 將預設閘道指派給連接至虛擬機器的第一個 (主要) 網路介面。 Azure 不會將預設閘道指派給連接至虛擬機器的其他 (次要) 網路介面。 因此依預設，您無法與次要網路介面中子網路之外的資源進行通訊。 不過，次要網路介面可與它們的子網路之外的資源通訊。 若要次要網路介面與其子網路之外的資源通訊，請參閱[在具有多個網路介面的虛擬機器作業系統內路由](#routing-within-a virtual-machine-operating-system-with-multiple-network-interfaces)。

> [!WARNING]
> 若網路介面具有私人 IPv6 位址，則無法新增至現有的虛擬機器。 只有在建立虛擬機器時，才能將具有私人 IPv6 位址的網路介面新增至虛擬機器。 請參閱[網路介面 IP 位址](virtual-network-network-interface-addresses.md)，進一步瞭解指派 IP 位址給網路介面。

|工具|命令|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>檢視 VM 的網路介面

您可以檢視目前連接至 VM 的網路介面，以了解每個網路介面的組態，以及指派給每個網路介面的 IP 位址。 

1. 使用具備您訂用帳戶之擁有者、參與者或網路參與者角色的帳戶登入 [Azure 入口網站](https://portal.azure.com)。 若要深入了解將角色指派給帳戶的詳細資訊，請參閱 [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 Azure 入口網站頂端包含「搜尋資源」文字的方塊中，輸入「虛擬機器」。 當「虛擬機器」出現於搜尋結果時，按一下它。
3. 在顯示的 [虛擬機器] 刀鋒視窗中，按一下您要檢視其網路介面的 VM 名稱。
4. 在針對您所選 VM 出現的 [虛擬機器] 刀鋒視窗中，於 [設定] 區段按一下 [網路服務]。 若要了解網路介面設定以及如何變更它們，請閱讀[管理網路介面](virtual-network-network-interface.md)一文。 若要了解如何新增、變更或移除已指派給網路介面的 IP 位址，請參閱[管理 IP 位址](virtual-network-network-interface-addresses.md)。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>從 VM 移除網路介面

您需要從中移除 (或中斷連結) 網路介面的 VM 必須處於已停止 (已解除配置) 狀態，而且目前必須至少有兩個連結的網路介面。 您可以移除任何網路介面，但 VM 一律至少必須有一個連接的網路介面。 如果您移除主要網路介面，Azure 會將主要屬性指派給連接至 VM 的時間最久的網路介面。 

1. 使用具備您訂用帳戶之擁有者、參與者或網路參與者角色的帳戶登入 [Azure 入口網站](https://portal.azure.com)。 若要深入了解將角色指派給帳戶的詳細資訊，請參閱 [Azure 角色型存取控制的內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)。
2. 在 Azure 入口網站頂端包含「搜尋資源」文字的方塊中，輸入「虛擬機器」。 當「虛擬機器」出現於搜尋結果時，按一下它。
3. 在出現的 [虛擬機器] 刀鋒視窗中，按一下您需要移除其網路介面的 VM 名稱。
4. 在針對您所選 VM 出現的 [虛擬機器] 刀鋒視窗中，於 [設定] 區段按一下 [網路服務]。 若要了解網路介面設定以及如何變更它們，請閱讀[管理網路介面](virtual-network-network-interface.md)一文。 若要了解如何新增、變更或移除已指派給網路介面的 IP 位址，請參閱[管理 IP 位址](virtual-network-network-interface-addresses.md)。
5. 按一下 [X 中斷連結網路介面]。
6. 選取您想要從下拉式清單中卸除的網路介面，然後按一下 [確定]。

**命令**

|工具|命令|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (參考) 或[詳細步驟](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (參考) 或[詳細步驟](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>接續步驟
若要建立具有多個網路介面或 IP 位址的 VM，請閱讀下列文章：

**命令**

|Task|工具|
|---|---|
|建立具有多個 NIC 的 VM|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|建立具有多個 IPv4 位址的單一 NIC VM|[CLI](virtual-network-multiple-ip-addresses-cli.md)、[PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|建立具有私人 IPv6 位址的單一 NIC VM (在 Azure Load Balancer 後端)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json)、[Azure Resource Manager 範本](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
