---
title: セキュリティで保護された MOR 実装
description: MemoryOverwriteRequestControlLock UEFI 変数 revision 2 の動作と使用法について説明します。
ms.assetid: 94F42629-3B76-4EB1-A5FA-4FA13C932CED
ms.date: 01/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 67296395acd0e9a83c2c5dd71b3459854fd59ce1
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769398"
---
# <a name="secure-mor-implementation"></a>セキュリティで保護された MOR 実装

## <a name="summary"></a>要約

- MorLock の動作、リビジョン2

## <a name="last-updated"></a>最終更新日

- 2018 年 1 月

## <a name="applies-to"></a>適用対象

- Windows 10

- Windows 10 の Credential Guard 機能をサポートする Oem および BIOS ベンダー。

## <a name="official-specifications"></a>公式の仕様

- [UEFI 仕様](https://uefi.org/specifications)

- [PC クライアントの作業グループプラットフォームのリセット攻撃の緩和の仕様、バージョン 1.0 (PDF のダウンロード)](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

## <a name="recommended-reading"></a>推奨資料

- [ブログの投稿: コールド攻撃 (およびその他の脅威) からの BitLocker の保護](https://docs.microsoft.com/archive/blogs/si_team/protecting-bitlocker-from-cold-attacks-and-other-threats)

- [ホワイトペーパー: EDKII での UEFI TPM2 のサポートを備えた BIOS 以外のツアー](https://github.com/tianocore/edk2-platforms/blob/devel-MinPlatform/Platform/Intel/MinPlatformPkg/Docs/A_Tour_Beyond_BIOS_Open_Source_IA_Firmware_Platform_Design_Guide_in_EFI_Developer_Kit_II%20-%20V2.pdf)

- [Credential Guard によるドメインの派生資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)

## <a name="overview"></a>概要

このトピックでは、UEFI 変数 revision 2 の動作と使用法について説明し `MemoryOverwriteRequestControlLock` ます。

高度なメモリ攻撃を防ぐために、既存のシステム BIOS のセキュリティ対策**MemoryOverwriteRequestControl**が改善され、新しい脅威から保護するためのロックがサポートされるようになりました。  脅威モデルは、ホスト OS カーネルを敵対者として追加するために拡張されているため、カーネル特権レベルで実行されている ACPI および UEFI ランタイムサービスは信頼されていません。  セキュアブート実装と同様に、MorLock は、ホスト OS カーネル (システム管理モード、TrustZone、BMC など) によって改ざんされる特権のあるファームウェア実行コンテキストに実装する必要があります。  このインターフェイスは UEFI 変数サービスに基づいて構築されています。これについては、UEFI 仕様バージョン2.5 で説明されています。 "Variable Services" という名前のセクション7.2 を参照してください。

*Morlock*と呼ばれるこの軽減策は、すべての新しいシステムに実装する必要があり、信頼されたプラットフォームモジュールを持つシステムに限定されるだけではありません。 リビジョン2では、起動時のパフォーマンスの問題を軽減するために、新しい機能である*ロック解除*を追加します。特に、大規模なメモリシステムでは、

\_MOR bit 状態を設定するための ACPI DSM の制御方法については、「 [PC クライアントの作業グループプラットフォームのリセット攻撃の回避仕様、バージョン 1.0 (PDF のダウンロード)](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)」で説明されているように、この \_ dsm メソッドを最新の BIOS 実装から削除することをお勧めします。  ただし、BIOS がこの DSM メソッドを実装する場合は、 \_ MorLock の状態を尊重する必要があります。  キーがあるかどうかにかかわらず、MorLock がロックされている場合、この \_ DSM メソッドは MOR を変更できず、"一般エラー" に対応する値1を返す必要があります。  MorLock リビジョン2のロックを解除するための ACPI メカニズムが定義されていません。  

Windows は、windows 7 以降、この DSM メソッドを直接呼び出していないの \_ で、非推奨と見なされることに注意してください。  BIOS に*indirectly*よっ \_ ては、Windows が自動的にクリーンシャットダウンの実装として ACPI ポイントを呼び出すときに、この DSM メソッドが間接的に呼び出さ \_ れます (「 [PC クライアントの作業グループプラットフォームリセット攻撃の仕様、バージョン 1.0 (PDF ダウンロード)](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)」のセクション2.3 を参照)。  

この ACPI \_ PTS での MOR 自動検出の実装はセキュリティ短さであるため、使用しないでください。

## <a name="memoryoverwriterequestcontrollock"></a>MemoryOverwriteRequestControlLock

改善された軽減策を含む BIOS は、初期ブート時にこの UEFI 変数を作成します。

**VendorGuid:**`{BB983CCF-151D-40E1-A07B-4A17BE168292}`

**名前:**`MemoryOverwriteRequestControlLock`

**属性:** NV + BS + RT

*データ*パラメーターの**getvariable**値: 0x0 (ロック解除);0x1 (キーなしでロック);0x2 (キーでロック)

*データ*パラメーターの**setvariable**値: 0x0 (ロック解除);0x1 (ロック)

## <a name="locking-with-setvariable"></a>SetVariable によるロック

すべてのブートで、BIOS は `MemoryOverwriteRequestControlLock` ブートデバイス選択 (BDS) フェーズ (ドライバー *unlocked* \# \# \# \# 、SYSPREP \# \# \# \# 、ブート \# \# \# \# 、 \* 回復 \* 、...) の前に、0x00 (ロック解除を示す) の1バイト値に初期化します。 `MemoryOverwriteRequestControlLock`(および) の場合 `MemoryOverwriteRequestControl` 、BIOS は変数と属性の削除を NV + BS + RT に固定する必要があります。

の**Setvariable** `MemoryOverwriteRequestControlLock` が、*データ*で0以外の有効な値を渡すことによって最初に呼び出された場合、との両方のアクセスモード `MemoryOverwriteRequestControlLock` `MemoryOverwriteRequestControl` が読み取り専用に変更され、ロックされていることが示されます。

Revision 1 の実装では、に対して1バイトの0x00 または0x01 のみを受け入れ `MemoryOverwriteRequestControlLock` ます。

さらに、リビジョン2では、共有シークレットキーを表す8バイトの値も受け入れられます。 **Setvariable**に他の値が指定されている場合は、status EFI INVALID パラメーターで呼び出しが失敗し \_ \_ ます。 このキーを生成するには、トラステッドプラットフォームモジュールやハードウェアの乱数ジェネレーターなどの高品質のエントロピソースを使用します。

キーを設定した後、呼び出し元とファームウェアの両方で、このキーのコピーを機密性の保護された場所 (IA32/X64 の場合は SMRAM、保護された記憶域を使用するサービスプロセッサなど) に保存する必要があります。

## <a name="getting-the-system-state"></a>システム状態の取得

リビジョン2では、 `MemoryOverwriteRequestControlLock` 変数と `MemoryOverwriteRequestControl` 変数がロックされている場合、(これらの変数の) **setvariable**の呼び出しは、最初に、定数時間アルゴリズムを使用して、登録されたキーに対してチェックされます。 両方のキーが存在し、一致する場合、変数はロック解除された状態に戻ります。 この最初の試行の後、またはキーが登録されていない場合、この変数を設定しようとすると、 \_ \_ ブルートフォース攻撃を防ぐために EFI アクセス拒否によって失敗します。 その場合、システムの再起動は、変数のロックを解除する唯一の方法である必要があります。

オペレーティングシステムは、 `MemoryOverwriteRequestControlLock` **getvariable**を呼び出して、とその状態の存在を検出します。 システムは、値を0x1 に設定して、の現在の値をロックでき `MemoryOverwriteRequestControl` `MemoryOverwriteRequestControlLock` ます。 または、シークレットデータがメモリから安全に消去された後で、今後、ロック解除を有効にするキーを指定することもできます。

に対して**Getvariable**を呼び出すと、ロック `MemoryOverwriteRequestControlLock` の解除、キーのないロック、またはキーの状態でロックされていることを示す0x0、0x1、または0x2 が返されます。

`MemoryOverwriteRequestControlLock`を設定しても、フラッシュはコミットされません (内部ロック状態を変更するだけです)。 変数を取得すると、内部状態が返され、キーを公開しません。

オペレーティングシステムによる使用例:

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

SetVariable(MemoryOverwriteRequestControlLock, 8, keyPtr);
```

## <a name="morlock-implementation-flow"></a>MorLock の実装フロー

これらのフローチャートは、実装の予想される動作を示しています。

### <a name="initialization"></a>初期化

![morlock の初期化](images/morlock.png)

### <a name="setvariable-flow"></a>SetVariable フロー

![morlock プログラミングフロー](images/morlock1.png)

### <a name="unlocked-state-flow-for-setvariable"></a>SetVariable のロック解除状態フロー

![morlock のロック解除フロー](images/morlock2.png)

### <a name="locked-state-flow-for-setvariable"></a>SetVariable のロック状態フロー

![morlock ロックフロー](images/morlock3.png)

### <a name="flow-for-getvariable"></a>GetVariable の Flow

![morlock getvariable](images/morlock4.png)

## <a name="see-also"></a>関連項目

[SoC プラットフォーム上のすべての Windows エディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md#security-requirements)

[PC クライアントの作業グループプラットフォームのリセット攻撃の緩和の仕様、バージョン 1.0 (PDF のダウンロード)](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)  

[コールド攻撃 (およびその他の脅威) からの BitLocker の保護](https://docs.microsoft.com/archive/blogs/si_team/protecting-bitlocker-from-cold-attacks-and-other-threats)  

[EDKII での UEFI TPM2 サポートを使用した BIOS に関するツアー](https://github.com/tianocore/edk2-platforms/blob/devel-MinPlatform/Platform/Intel/MinPlatformPkg/Docs/A_Tour_Beyond_BIOS_Open_Source_IA_Firmware_Platform_Design_Guide_in_EFI_Developer_Kit_II%20-%20V2.pdf)

[Credential Guard によるドメインの派生資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)

[UEFI 仕様](https://uefi.org/specifications)  
