---
title: セキュリティで保護された MOR 実装
description: 動作および MemoryOverwriteRequestControlLock UEFI 変数、リビジョン 2 の使用について説明します。
ms.assetid: 94F42629-3B76-4EB1-A5FA-4FA13C932CED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2beead842d1b671b84de6eb0ea167d88534417e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328093"
---
# <a name="secure-mor-implementation"></a>セキュリティで保護された MOR 実装


**要約**

-   MorLock、リビジョン 2 の動作

**最終更新日**

-   2018 年 1 月

**適用対象**

-   Windows 10
-   Windows 10 の Credential Guard 機能をサポートする Oem と BIOS のベンダー。

**公式の仕様**

-   [UEFI 仕様に準拠](https://go.microsoft.com/fwlink/p/?LinkId=717873)
-   [PC クライアント作業グループ プラットフォーム リセット攻撃軽減策仕様、バージョン 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)

**推奨資料**

-   [ブログの投稿:コールド攻撃 (およびその他の脅威) から BitLocker の保護]( https://go.microsoft.com/fwlink/p/?LinkId=717871)
-   [ホワイト ペーパー:EDKII で BIOS、UEFI TPM2 サポート外のツアー]( https://go.microsoft.com/fwlink/p/?LinkId=717872)
-   [Credential Guard によるドメインの派生資格情報の保護]( https://go.microsoft.com/fwlink/p/?LinkId=717899)

使用状況と動作について説明します、 `MemoryOverwriteRequestControlLock` UEFI 変数、リビジョン 2。

高度なメモリを防ぐために攻撃、既存のシステム BIOS のセキュリティ対策**MemoryOverwriteRequestControl**ロック新たな脅威に対する防御をサポートするが向上します。  脅威モデルは、敵対者として、ホスト OS カーネルのように拡張は、したがって ACPI およびカーネルの特権レベルで実行する UEFI ランタイム サービスが信頼されていません。  セキュア ブートの実装と同様に、MorLock は (たとえば、システム管理モード、TrustZone、BMC、およびなど) は、ホスト OS カーネルによって改ざんされない特権ファームウェアの実行コンテキストをで実装する必要があります。  インターフェイスは、UEFI 仕様バージョン 2.5 では、「変数サービス」という名前のセクション 7.2 で説明されている UEFI 変数サービスに基づいて構築されています。

**注**  と呼ばれるこの緩和策*MorLock*、すべての新しいシステムに実装されだけでなく、トラステッド プラットフォーム モジュールをシステムに制限する必要があります。 リビジョン 2 は、新しい機能を追加します*のロックを解除*、特に大容量メモリ システムで、ブート パフォーマンスの問題を軽減するためにします。

**注 2**  に関する、ACPI \_DSM コントロールのメソッド、されますを設定するビットの状態 (セクション 6 の説明に従って[PC クライアント作業グループ プラットフォーム リセット攻撃軽減策の仕様、バージョン 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)):  
Microsoft では、これを削除することをお勧め\_DSM メソッド最新の BIOS の実装から。  ただし、これを BIOS が実装されている場合\_DSM メソッド、MorLock の状態を考慮する必要があります。  MorLock がロックされている、またはキーがない場合この\_されますを変更し、「一般的なエラー」に対応する 1 つの値を返す DSM メソッドが失敗する必要があります。  MorLock リビジョン 2 のロックを解除する ACPI メカニズムが定義されていません。  Windows が呼び出されないこと直接この注\_Windows 7 以降の DSM メソッドと、非推奨と見なされます。  一部の BIOS*間接的*これを呼び出す\_DSM メソッドが呼び出す ACPI の Windows と\_されます自動検出のクリーン シャット ダウンの実装として PTS (」の「2.3 の説明に従って[PC クライアントの作業プラットフォームのリセット攻撃軽減策の仕様、バージョン 1.0 をグループ化](https://go.microsoft.com/fwlink/p/?LinkId=717870))。  この ACPI\_されますの自動検出の PTS 実装が不十分なセキュリティとは使用できません。

## <a name="memoryoverwriterequestcontrollock"></a>MemoryOverwriteRequestControlLock


強化された軽減策を含む BIOS では、ブート プロセスの初期中にこの UEFI 変数を作成します。

**VendorGuid:** `{BB983CCF-151D-40E1-A07B-4A17BE168292}`

**名:** `MemoryOverwriteRequestControlLock`

**属性:** NV + B キーを押しながら RT

**GetVariable**値*データ*パラメーター。0x0 (ロック)。0x1 (キーのないロック)。0x2 (キーを持つロック)

**SetVariable**値*データ*パラメーター。0x0 (ロック)。0x1 (ロック)

## <a name="locking-with-setvariable"></a>SetVariable のロック


起動のたびに BIOS が初期化されます`MemoryOverwriteRequestControlLock`0x00 の 1 バイト値に (示す*ロックされていない*) ブート デバイスの選択 (BDS) フェーズの前に (ドライバー\# \# \# \#、SYSPREP\#\#\#\#、ブート\#\#\#\#、 \*RECOVERY\*,...)。 `MemoryOverwriteRequestControlLock` (と`MemoryOverwriteRequestControl`) BIOS が、変数の削除を防ぐものと、属性は、NV + B キーを押しながら RT にピン留めする必要があります。

ときに**SetVariable**の`MemoryOverwriteRequestControlLock`で有効な 0 以外の値を渡すことによって最初に呼び出された*データ*、両方のアクセス モード`MemoryOverwriteRequestControlLock`と`MemoryOverwriteRequestControl`読み取り専用を示すにはあるロックされます。

リビジョン 1 実装は 0x00 またはの 0x01 の 1 バイトだけを受け入れる`MemoryOverwriteRequestControlLock`します。

リビジョン 2 は、さらに、共有シークレット キーを表す 8 バイトの値を受け入れます。 その他の値が指定されている場合**SetVariable**、EFI の状態で失敗する\_無効な\_パラメーター。 そのキーを生成するには、トラステッド プラットフォーム モジュール、またはハードウェア乱数ジェネレーターなど、質の高いエントロピのソースを使用します。

キーを設定した後、呼び出し元とファームウェアは SMRAM IA32/X 64 上で保護された記憶域を備えたサービス プロセッサなどの機密性が保護された場所にこのキーのコピーを保存する必要があります。

## <a name="getting-the-system-state"></a>システム状態を取得します。


リビジョン 2、ときに、`MemoryOverwriteRequestControlLock`と`MemoryOverwriteRequestControl`変数がロックされ、呼び出しの**SetVariable** (これらの変数) の最初に照合登録済みのキー一定時間のアルゴリズムを使用しています。 両方のキーが存在すると一致する場合、変数の移行はロック解除の状態に戻ります。 Efi を搭載したこの最初の試行後、またはキーが登録されていない場合は、この変数を設定する後続の試行が失敗する\_アクセス\_ブルート フォース攻撃を防ぐことが拒否されました。 その場合は、システムの再起動は、変数のロックを解除する唯一の方法になります。

オペレーティング システムの存在を検出する`MemoryOverwriteRequestControlLock`とその状態を呼び出して**GetVariable**します。 システムの現在の値をロックできます`MemoryOverwriteRequestControl`を設定して、 `MemoryOverwriteRequestControlLock` 0x1 の値。 または、機密データがメモリから安全に削除された後、将来のロック解除を有効にするキーを指定、可能性があります。

呼び出す**GetVariable**の`MemoryOverwriteRequestControlLock`0x0、0x1、または 0x2 を示す、ロックを解除、キーのないロックされているか、キーの状態でロックを返します。

**注**  設定`MemoryOverwriteRequestControlLock`flash にコミットしない (内部ロック状態を変更するだけです)。 変数の取得、内部の状態を返すし、キーは公開されません。 次の図では、想定される動作について説明します。

 

オペレーティング システムでの使用例

```cpp
if (gSecretsInMemory) 
{
    char data = 0x11;
    SetVariable(MemoryOverwriteRequestControl, sizeof(data), &data);
}
 
// check presence
status = GetVariable(MemoryOverwriteRequestControlLock, &value);  
    
if (SUCCESS(status)) 
{
    // first attempt to lock and establish a key 
    // note both MOR and MorLock are locked if successful

    GetRNG(8, keyPtr);
    status = SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr); 

    if (status != EFI_SUCCESS) 
    {
        // fallback to revision 1 behavior
        char data = 0x01;
        status = SetVariable(MemoryOverwriteRequestControlLock, 1, &data); 
        if (status != EFI_SUCCESS) { // log error, warn user }
    }
} 
else 
{
    // warn user about potentially unsafe system
}

// put secrets in memory

// … time passes …

// remove secrets from memory, flush caches

SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr)
```

## <a name="morlock-implementation-flow"></a>MorLock 実装のフロー


これらのフローチャートは、実装の想定される動作を示します。

### <a name="initialization"></a>初期化

![morlock 初期化](images/morlock.png)

### <a name="setvariable-flow"></a>SetVariable フロー

![morlock プログラミング フロー](images/morlock1.png)

### <a name="unlocked-state-flow-for-setvariable"></a>SetVariable のロック解除状態のフロー

![ロックを解除 morlock フロー](images/morlock2.png)

### <a name="locked-state-flow-for-setvariable"></a>SetVariable の状態のフローがロックされています。

![ロックされている morlock フロー](images/morlock3.png)

### <a name="flow-for-getvariable"></a>GetVariable のフロー

![morlock getvariable](images/morlock4.png)

## <a name="related-topics"></a>関連トピック
[SoC のプラットフォームですべての Windows エディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md#security-requirements)  
[PC クライアント作業グループ プラットフォーム リセット攻撃軽減策仕様、バージョン 1.0](https://go.microsoft.com/fwlink/p/?LinkId=717870)  
[コールド攻撃 (およびその他の脅威) から BitLocker の保護]( https://go.microsoft.com/fwlink/p/?LinkId=717871)  
[EDKII で BIOS、UEFI TPM2 サポート外のツアー]( https://go.microsoft.com/fwlink/p/?LinkId=717872)  
[Credential Guard によるドメインの派生資格情報の保護]( https://go.microsoft.com/fwlink/p/?LinkId=717899)  
[UEFI 仕様に準拠](https://go.microsoft.com/fwlink/p/?LinkId=717873)  



