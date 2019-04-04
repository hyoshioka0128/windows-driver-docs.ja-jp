---
title: VMQ フィルタの設定
description: VMQ フィルタの設定
ms.assetid: d40b6806-6ba8-4073-b802-57cb886ffcfb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da692ecad229f9aa87d9a288db66573faf1badda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553933"
---
# <a name="setting-a-vmq-filter"></a>VMQ フィルタの設定


受信キューが割り当てられた後、後続のドライバーと、フィルターが受信キューに設定できます。 受信キューを割り当て、ドライバーは、そのキューにフィルターを設定できます。

**注**  ため、既定の受信キュー (**NDIS\_既定\_受信\_キュー\_ID**) 常に存在する、常に設定できるドライバーが重なって、既定のキューにフィルターが表示されます。 上にあるドライバーは、既定のキューを所有していません。 そのため、ネットワーク アダプターにバインドされているすべてのプロトコル ドライバーには、既定のキューを使用できます。

 

## <a name="setting-a-filter-on-a-receive-queue"></a>受信キューにフィルターを設定


上位のドライバーの問題を初期構成パラメーターのセットの受信キューにフィルターを設定する、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)メソッド オブジェクト識別子 (OID) 要求します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体は、初期状態へのポインターを含む、 [**NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。 OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 **NDIS\_OID\_要求**構造体にはへのポインターが含まれています、 **NDIS\_受信\_フィルター\_パラメーター**新しいフィルターの識別子を持つ構造体。

上にあるドライバーを初期化します、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体の次のフィルターの構成パラメーターを使用して、キューが表示されます。

-   指定されたフィルターの種類、 [ **NDIS\_受信\_フィルター\_型**](https://msdn.microsoft.com/library/windows/hardware/ff567186)列挙値。

    **注**  NDIS 6.20 が動作をのみ以降**NdisReceiveFilterTypeVMQueue**仮想マシン キュー (VMQ) インターフェイスのフィルターの種類がサポートされています。

     

-   キューの識別子です。

-   として書式設定されている 1 つまたは複数のフィールド テスト パラメーター [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体。 VMQ、次のフィールドのテスト パラメーターが定義されます。

    -   パケットの宛先メディア アクセス制御 (MAC) アドレスでは、指定された MAC アドレスと同じです。

    -   パケット内の仮想 LAN (VLAN) 識別子では、指定した VLAN 識別子と同じです。

[ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体を併用、 [OID\_受信\_フィルター\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569792) OID と[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)の構成パラメーターを指定する OID、フィルターです。

**FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、および**FieldParametersArrayElementSize**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体の配列を定義する[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体。 各**NDIS\_受信\_フィルター\_フィールド\_パラメーター**配列内の構造は、ネットワーク ヘッダーで 1 つのフィールドのフィルターのテスト条件を設定します。

**フラグ**のメンバー、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体を指定します受信フィルターに対して実行するアクション。 次の点を適用する、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フラグ。

-   場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグに設定されて、**フラグ**のメンバー、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造、ネットワーク アダプターは、次のテスト条件のすべてに一致する受信パケットのみを示す必要があります。

    -   一致する MAC アドレスを持つパケットです。

    -   VLAN タグがない場合や 0 の VLAN 識別子を持つパケット。

    場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグが設定されて、ネットワーク アダプターが一致する MAC アドレスと 0 以外の場合、VLAN 識別子を持つパケットを示す必要がありますされません。

    **注**  HYPER-V 拡張可能スイッチは、MAC アドレス フィルターを設定しで VLAN 識別子フィルターが構成されていない場合[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)、スイッチが設定も、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フラグ。

     

-   場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグが設定されていないの OID セット要求によって構成されている VLAN 識別子フィルターがない[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)、ミニポート ドライバー次のいずれかを実行する必要があります。

    -   OID 要求の失敗した状態を返す必要があります、ミニポート ドライバーでは、NDIS 6.20 が動作をサポートする場合[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。

    -   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーをサポートする場合を検査し、指定された MAC アドレスのフィールドをフィルター処理するネットワーク アダプターを構成する必要があります。 VLAN タグの受信パケットに存在する場合、ネットワーク アダプターする必要がありますから削除パケット データ。 ミニポート ドライバーに VLAN タグを配置する必要があります、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566565)関連付けられている、パケットの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

-   プロトコル ドライバーは、MAC アドレス フィルターと VLAN 識別子フィルターを設定する場合、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) OID は設定しません、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フラグフィルター フィールドのいずれか。 この場合、ミニポート ドライバーでは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 ミニポート ドライバーでは、0 の VLAN 識別子またはタグなしのパケットは MAC アドレスを一致するパケットが示されませんする必要があります。

## <a name="using-the-filter-identifier"></a>フィルターの識別子を使用してください。


NDIS フィルター識別子を割り当てます、 **FilterId**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体し、の OID メソッド要求を渡します[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)基になるミニポート ドライバーにします。 受信キューが設定されている各フィルターには、ネットワーク アダプターのフィルターの一意な識別子があります。 つまり、フィルターの識別子は、ネットワーク アダプターを管理する別のキューでは複製されません。

上にあるドライバーは、NDIS を以降の OID 要求で提供するフィルターの識別子を使用する必要があります。たとえば、次のようにフィルター パラメーターを変更するか、フィルターを解放するためです。

NDIS 受信キューにフィルターを設定する OID 要求を受け取ると、フィルター パラメーターを確認します。 NDIS は、必要なリソースとフィルターの識別子を割り当て後、は、基になるネットワーク アダプターに OID 要求を送信します。 OID を使用して要求が完了する場合は、ネットワーク アダプターは、フィルター、必要なソフトウェアとハードウェア リソースを割り当てることができますが正常に、 **NDIS\_状態\_成功**します。

ミニポート ドライバーでは、割り当てられた受信のフィルターのフィルターの識別子を保持する必要があります。 NDIS は、受信フィルター パラメーターを変更または受信のフィルターをクリアするには、以降の OID 要求フィルターのフィルターの識別子を使用します。 パラメーターを変更し、フィルターをクリアする方法の詳細については、[VM キュー パラメーターの更新の取得と](obtaining-and-updating-vm-queue-parameters.md)と[VMQ フィルターをクリア](clearing-a-vmq-filter.md)を参照してください。

## <a name="handling-the-filter-on-a-receive-queue"></a>受信キューにフィルターを処理


ミニポート ドライバーでは、次のように、フィルターに基づくネットワーク アダプターをプログラムします。

-   特定のフィルターのすべてのフィールド テスト パラメーターは、パケットをキューに割り当てるには一致する必要があります。

-   複数のフィルターは、キューを設定できます。

-   フィルターのいずれかを渡す場合、パケットを受信キューに割り当てられる必要があります。

ネットワーク アダプターが論理フィールドのすべてのテストの結果をまとめて**AND**操作。 任意のフィールドをテストする場合は、配列に含まれる、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)失敗した場合、構造体、ネットワーク パケットが、指定したフィルター条件を満たしていません。

ネットワーク アダプターでは、これらのフィルター条件に対して受信したパケットをテストは、テスト条件の指定がない、パケット内のすべてのフィールドを無視する必要があります。

## <a name="receiving-packets-from-a-receive-queue"></a>受信キューからのパケットの受信


ドライバーの受信後、ミニポート、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)要求、キューに設定されているフィルター、キューが*を実行している*状態。 キューは、この状態では、ミニポート ドライバーでは、キュー上のパケットを指定できます。 キューの状態の詳細については、[キューの状態と操作](queue-states-and-operations.md)を参照してください。

ミニポート ドライバーが受信した場合、 [OID\_受信\_フィルター\_キュー\_割り当て\_完了](https://msdn.microsoft.com/library/windows/hardware/ff569793)OID がキューの要求が、フィルターのセットがない、キュー、ミニポート ドライバー示す必要がありますいないそのキューでパケットを受信していずれか。 この場合、ミニポート ドライバーを受け取ると、 [OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795) OID は、キューの要求し、OID 要求が完了すると、前に、可能な限りそのキュー上のパケットを示します。 OID を処理している間、ミニポート ドライバーをキューにパケットを示している場合\_受信\_フィルター\_設定\_フィルター OID 要求、ミニポート ドライバーが、OID を完了する必要があります\_受信\_フィルター\_設定\_がフィルターの要求、 **NDIS\_状態\_成功**コードが返されます。

 

 





