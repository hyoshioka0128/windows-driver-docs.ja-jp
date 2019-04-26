---
title: パケット結合受信フィルターの指定
description: パケット結合受信フィルターの指定
ms.assetid: 0369A63D-4CDE-448A-8472-EEEB7B859B8D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384e3acaeecaf2f7730dd854ee4e352f964bfe67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355210"
---
# <a name="specifying-a-packet-coalescing-receive-filter"></a>パケット結合受信フィルターの指定


以上の受信 NDIS パケットの結合をサポートするミニポート ドライバーのフィルターまたは上位のドライバーが 1 つを設定できます。 上にあるドライバーは、ミニポート ドライバーがで指定された受信フィルターの最大数まで指定できます、 **MaxPacketCoalescingFilters**のメンバー、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)構造体。

**注**  上位プロトコル ドライバーを取得、 [ **NDIS\_受信\_フィルター\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)内で構造体、[ **NDIS\_バインド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff564832)構造体。 上にあるフィルター ドライバーを取得、 **NDIS\_受信\_フィルター\_機能**内で構造体、 [ **NDIS\_フィルター\_アタッチ\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565481)構造体。

 

上にあるドライバーのダウンロードの OID メソッド要求を発行してミニポート ドライバーにフィルターが表示される[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)この OID 要求へのポインターが含まれている構造体、呼び出し元が割り当てたバッファー。 このバッファーは、以下を格納する形式です。

-   [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181) NDIS のパラメーターを指定する構造体は、フィルターを受信します。

    この構造体を初期化する方法の詳細については、次を参照してください。[受信フィルターを指定する](#specifying-receive-filter)します。

-   配列の[ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)フィルターを指定する構造体のフィールドの条件をテストします。ネットワーク パケットのヘッダー。

    これらの構造体を初期化する方法の詳細については、次を参照してください。[ヘッダー フィールドのテストを指定する](#specifying-header-field-test)します。

## <a name="specifying-a-receive-filter"></a>受信フィルターを指定します。


上位のドライバーを初期化することにより受信パケットの結合フィルターを指定します、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体、フィルターの構成パラメーター。 初期化時、 **NDIS\_受信\_フィルター\_パラメーター**構造上にあるドライバーがこれらの規則に従う必要があります。

-   **FilterType**にメンバーを設定する必要があります、 [ **NDIS\_受信\_フィルター\_型**](https://msdn.microsoft.com/library/windows/hardware/ff567186) の列挙値**NdisReceiveFilterTypePacketCoalescing**します。

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

    **注**  NDIS 6.30 以降では、受信パケットの結合フィルターは、既定でのみサポート、ネットワーク アダプターのキューの受信します。 この受信キューが識別子の NDIS\_既定\_受信\_キュー\_id。

     

-   上にあるドライバーが、新しい受信フィルターを作成する場合に設定する必要があります、 **FilterId** NDIS メンバー\_既定\_受信\_フィルター\_id。

    **注**  NDIS では、フィルターの一意の識別子 (ID) の生成、受信フィルターの OID メソッド要求を転送する前に[OID\_受信\_フィルター\_セット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)ミニポート ドライバーにします。     

-  上にあるドライバーは、既存の受信フィルターを変更することは場合に、設定する必要があります、 **FilterId**受信フィルターの 0 以外のフィルター ID にメンバー。 上にあるドライバーの OID メソッド要求を発行するときに受信フィルターのフィルター ID を取得します[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)します。 受信フィルターを変更する方法の詳細については、次を参照してください。[変更パケット結合受信フィルター](modifying-packet-coalescing-receive-filters.md)します。

-   **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、および**FieldParametersArrayElementSize**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)フィールド パラメーターの配列を定義する構造体を設定する必要があります。 配列内の各要素は、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)ヘッダーのパラメーターを指定する構造体受信フィルターのフィールドのテスト。

-   **RequestedFilterIdBitCount**メンバーは 0 に設定する必要があります。

-   **MaxCoalescingDelay**受信フィルターに一致する最初のパケットが保存され、ネットワーク アダプターの 1 つにまとめ、最大時間 (ミリ秒単位) の単位を設定する必要があります。 フィルターに一致する最初のパケットを受信するとすぐにネットワーク アダプターにパケットを連結しが有効期限は、の値に設定されてハードウェア タイマーが開始、 **MaxCoalescingDelay**メンバー。

上にあるドライバーは、MAC、およびプロトコルの関連付けられているヘッダーは、パケットに存在することと同じ順序でフィールド パラメーター配列でヘッダー フィールド テストを順序付けする必要があります。

たとえば、上にあるドライバーは、フィルター パラメーターを指定する前に、ip version 4 (IPv4) プロトコルのフィールド、MAC ヘッダーの protocol フィールド (NdisMacHeaderFieldProtocol) のフィルター パラメーターをまず指定する必要があります。 この方法では、ドライバーは、IPv4 パケットの正しい EtherType 値 (0x0800) にフィールドを検証するテストのヘッダー フィールドが設定されているを指定します。 テストに失敗した場合、アダプターが IPV4 プロトコル フィールドのテストを行うことはありません。

## <a name="specifying-header-field-tests"></a>ヘッダー フィールド テストを指定します。


各受信フィルターが 1 つまたは複数のテスト条件を指定できます (*ヘッダー フィールド テスト*)。 ネットワーク アダプターは、アダプターのハードウェア合体バッファーで受信したパケットを結合する必要があるかどうかを判断するこれらのテストを実行します。 また、上にあるドライバーを指定できます別個のフィルターのテストのさまざまなメディア アクセス制御 (MAC)、IP version 4 (IPv4) と IP version 6 (IPv6) のヘッダー フィールド。

ネットワーク アダプターのフィルター処理を最適化するには、ヘッダー フィールドのテストは、パケット データ内のバイト オフセットと長さの仕様ではなく、標準化されたヘッダー フィールド名に基づいています。 ヘッダー/フィールド名を使用すると、ネットワーク アダプターのハードウェアまたはファームウェアを最適化できます受信パケットのヘッダー フィールドの複数のテストが実行されます。

各受信フィルターで指定された 1 つまたは複数のヘッダー フィールド テストを含めることができます、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造体。 各**NDIS\_受信\_フィルター\_フィールド\_パラメーター**構造によって参照されるフィールド パラメーター配列の要素である、 **FieldParametersArrayOffset**、 **FieldParametersArrayNumElements**、および**FieldParametersArrayElementSize**のメンバー、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体。

ミニポート ドライバーは、の OID メソッド要求を処理する場合これらのガイドラインに従う必要があります[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795):

-   場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグに設定されて、**フラグ**のメンバー、 [ **NDIS\_受信\_フィルター\_フィールド\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff567169)構造、ネットワーク アダプターには、MAC アドレスが一致する、タグなしのパケットの受信パケットまたは 0 の VLAN 識別子を持つパケットのみを示す必要があります。 ネットワーク アダプターでは、パケットは MAC アドレスが一致する、0 以外の場合、VLAN 識別子が示されませんする必要があります。

-   場合、 **NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_ゼロ**フラグが設定されていないの OID セット要求によって構成されている VLAN 識別子フィルターがない[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)、ミニポート ドライバー次のいずれかを実行する必要があります。

    -   OID 要求の失敗した状態を返す必要があります、ミニポート ドライバーでは、NDIS 6.20 が動作をサポートする場合[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)します。

    -   NDIS 6.30 または以降のバージョンの NDIS ミニポート ドライバーをサポートする場合を検査し、指定された MAC アドレスのフィールドをフィルター処理するネットワーク アダプターを構成する必要があります。 VLAN タグの受信パケットに存在する場合、ネットワーク アダプターする必要がありますから削除パケット データ。 ミニポート ドライバーに VLAN タグを配置する必要があります、 [ **NDIS\_NET\_バッファー\_一覧\_8021Q\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff566565)関連付けられている、パケットの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

-   MAC アドレス フィルターと VLAN 識別子フィルターで上にあるドライバーが設定されている場合、 [ **NDIS\_受信\_フィルター\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567181)構造体を設定しません**NDIS\_受信\_フィルター\_フィールド\_MAC\_ヘッダー\_VLAN\_UNTAGGED\_または\_0**フィルター フィールドのいずれかのフラグ。 この場合、ミニポート ドライバーでは、指定された MAC アドレスと VLAN 識別子の両方に一致するパケットを示す必要があります。 ミニポート ドライバーでは、0 の VLAN 識別子またはタグなしのパケットは MAC アドレスを一致するパケットが示されませんする必要があります。

 

 





