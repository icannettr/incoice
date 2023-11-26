# icannettr UBL-Invoice Generator

sabre/xml Kütüphanesine ihtiyaç duyuyor.

1. Direk Kullanım Örneği   
      ```php
       $invoice = (new \icannettr\invoice\Invoice())
            ->setUBLVersionID("2.1")
            ->setCustomizationID("TR1.2")
            ->setProfileID("TEMELFATURA")
            ->setId("GIB20090000000001")
            ->setCopyIndicator(false)
            ->setUUID("F47AC10B-58CC-4372-A567-0E02B2C3D479")
            ->setIssueDate("2009-01-05")
            ->setIssueTime("14:42:00")
            ->setInvoiceTypeCode(\icannettr\invoice\InvoiceTypeCode::SATIS)
            ->setDocumentCurrencyCode("TRY")
            ->setLineCountNumeric("1")
            ->setInvoicePeriod(
                (new \icannettr\invoice\InvoicePeriod())
                    ->setStartDate("2008-12-05")
                    ->setEndDate("2009-01-05")
            )
            ->setSignature(
                (new \icannettr\invoice\Signature())
                    ->setVknTCKN("1288331521")
                    ->setSignatoryParty(
                        (new \icannettr\invoice\SignatoryParty())
                            ->setVkn("1288331521")
                            ->setPostalAddress(
                                (new \icannettr\invoice\Address())
                                    ->setStreetName("Papatya Caddesi Yasemin Sokak")
                                    ->setBuildingNumber("21")
                                    ->setCitySubdivisionName("Beşiktaş")
                                    ->setCityName("İSTANBUL")
                                    ->setPostalZone("34100")
                            )
                    )
                    ->setDigitalSignatureAttachmentURI("#Signature")
            )
            ->setAccountingSupplierParty(
                (new \icannettr\invoice\Party())
                    ->setName("AAA Anonim Şirketi")
                    ->setWebsiteURI("http://www.aaa.com.tr/")
                    ->setPostalAddress(
                        (new \icannettr\invoice\Address())
                            ->setStreetName("Papatya Caddesi Yasemin Sokak")
                            ->setBuildingNumber("21")
                            ->setCitySubdivisionName("Beşiktaş")
                            ->setCityName("İstanbul")
                            ->setPostalZone("34100")
                            ->setCountry(
                                (new \icannettr\invoice\Country())
                                    ->setName("Türkiye")
                            )
                    )->setContact(
                        (new \icannettr\invoice\Contact())
                            ->setTelephone("(212) 925 51515")
                            ->setTelefax("(212) 925505015")
                            ->setElectronicMail("aa@aaa.com.tr")
                    )->setPartyTaxScheme(
                        (new \icannettr\invoice\PartyTaxScheme())
                            ->setTaxScheme(
                                (new \icannettr\invoice\TaxScheme())
                                    ->setName("Büyük Mükellefler")
                            )
                    )->setPartyIdentifications(
                        [
                            (new \icannettr\invoice\PartyIdentification())->setValue("VKN", "1288331521")
                        ]
                    )
            )
            ->setAccountingCustomerParty(
                (new \icannettr\invoice\Party())
                    ->setName("Deneme")
                    ->setPostalAddress(
                        (new \icannettr\invoice\Address())
                            ->setStreetName("6. Sokak")
                            ->setBuildingNumber("1")
                            ->setCitySubdivisionName("Beşiktaş")
                            ->setCityName("İstanbul")
                            ->setPostalZone("34100")
                            ->setCountry(
                                (new \icannettr\invoice\Country())
                                    ->setName("Türkiye")
                            )
                    )->setContact(
                        (new \icannettr\invoice\Contact())
                            ->setElectronicMail("1234567890@mydn.com.tr")
                    )->setPerson(
                        (new \icannettr\invoice\Person())
                            ->setFirstName("Ali")
                            ->setFamilyName("YILMAZ")
                    )->setPartyIdentifications(
                        [
                            (new \icannettr\invoice\PartyIdentification())->setValue("TCKN", "1234567890"),
                            (new \icannettr\invoice\PartyIdentification())->setValue("TESISATNO", "1234567"),
                            (new \icannettr\invoice\PartyIdentification())->setValue("SAYACNO", "12345678")
                        ]
                    )
            )
            ->setPaymentTerms(
                (new \icannettr\invoice\PaymentTerms())->setNote("BBB Bank Otomatik Ödeme")->setPaymentDueDate("2009-01-20")
            )
            ->setTaxTotal(
                (new \icannettr\invoice\TaxTotal())->setTaxAmount(2.73)->addTaxSubTotal(
                    (new \icannettr\invoice\TaxSubTotal())->setTaxableAmount(15.15)->setTaxAmount(2.73)->setTaxCategory(
                        (new \icannettr\invoice\TaxCategory())->setTaxScheme(
                            (new \icannettr\invoice\TaxScheme())->setTaxTypeCode("0015")
                        )
                    )
                )
            )
            ->setLegalMonetaryTotal(
                (new \icannettr\invoice\LegalMonetaryTotal())
                    ->setLineExtensionAmount(15.15)
                    ->setTaxExclusiveAmount(15.15)
                    ->setTaxInclusiveAmount(17.88)
                    ->setPayableAmount(17.88)
            )
            ->setInvoiceLines([
                (new \icannettr\invoice\InvoiceLine())
                    ->setId("1")
                    ->setInvoicedQuantity(101)
                    ->setLineExtensionAmount(15.15)
                    ->setUnitCode("KWH") //BİZİM KULLANACAĞIMIZ C62
                    ->setTaxTotal(
                        (new \icannettr\invoice\TaxTotal())->setTaxAmount(2.73)->addTaxSubTotal(
                            (new \icannettr\invoice\TaxSubTotal())->setTaxableAmount(15.15)->setTaxAmount(2.73)->setPercent(18.0)->setTaxCategory(
                                (new \icannettr\invoice\TaxCategory())->setTaxScheme(
                                    (new \icannettr\invoice\TaxScheme())->setName("KDV")->setTaxTypeCode("0015")
                                )
                            )
                        )
                    )->setItem(
                        (new \icannettr\invoice\Item())->setName("Elektrik Tüketim Bedeli")
                    )
                    ->setPrice(
                        (new \icannettr\invoice\Price())->setPriceAmount(0.15)->setUnitCode("KWH")
                    )
            ]);
      // Test created object
      // Use \icannettr\invoice\Generator to generate an XML string
      $generator = new \icannettr\invoice\Generator();
      $outputXMLString = $generator->invoice($invoice);

      // Create PHP Native DomDocument object, that can be
      // used to validate the generate XML
      $dom = new \DOMDocument;
      $dom->loadXML($outputXMLString);

      $dom->save('KAYIT PATHI');
      ```
