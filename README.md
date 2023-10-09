if (stepCount === 4) {
        if (!isTextValid(currentStartEndOperationsData.recruiter)) {
          dispatch(
            setStartEndValidation(
              "recruiterValid",
              "Recruiter name should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.teamLead)) {
          dispatch(
            setStartEndValidation(
              "teamLeadValid",
              "Team lead name should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.crm)) {
          dispatch(
            setStartEndValidation("crmValid", "CRM should not be empty.")
          );
        }
        if (!isTextValid(currentStartEndOperationsData.teamManager)) {
          dispatch(
            setStartEndValidation(
              "teamManagerValid",
              "Team manager should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.seniorManager)) {
          dispatch(
            setStartEndValidation(
              "seniorManagerValid",
              "Senior manager should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.assoDirector)) {
          dispatch(
            setStartEndValidation(
              "assoDirectorValid",
              "Associate director should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.centerHead)) {
          dispatch(
            setStartEndValidation(
              "centerHeadValid",
              "Center head should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.onsiteAccDirector)) {
          dispatch(
            setStartEndValidation(
              "onsiteAccDirectorValid",
              "Onsite account director should not be empty."
            )
          );
        }
        if (!isTextValid(currentStartEndOperationsData.onboCoordinator)) {
          dispatch(
            setStartEndValidation(
              "onboCoordinatorValid",
              "Onboarding coordinator should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.endDate)) {
          dispatch(
            setStartEndValidation(
              "endDateValid",
              "End date should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.grossBr)) {
          dispatch(
            setStartEndValidation(
              "grossBrValid",
              "Gross BR should not be empty."
            )
          );
        }

        if (isTextValid(currentStartEndOperationsData.mspFeePercentage)) {
          dispatch(
            setStartEndValidation(
              "mspFeePercentageValid",
              "MSP fee in percentage should not be empty."
            )
          );
        }

        if (isTextValid(currentStartEndOperationsData.mspFee)) {
          dispatch(
            setStartEndValidation("mspFeeValid", "MSP fee should not be empty.")
          );
        }
        if (isTextValid(currentStartEndOperationsData.payRate)) {
          dispatch(
            setStartEndValidation(
              "payRateValid",
              "Pay rate should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.refFee)) {
          dispatch(
            setStartEndValidation(
              "refFeeValid",
              "Referral fee should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.taxOHPercentage)) {
          dispatch(
            setStartEndValidation(
              "taxOHPercentageValid",
              "Tax OH percentage should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.taxOH)) {
          dispatch(
            setStartEndValidation("taxOHValid", "Tax OH should not be empty.")
          );
        }
        if (isTextValid(currentStartEndOperationsData.hBenefitesOpted)) {
          dispatch(
            setStartEndValidation(
              "hBenefitesOptedValid",
              "Opted for health benefits should not be empty."
            )
          );
        }

        if (isTextValid(currentStartEndOperationsData.hBenefitesCost)) {
          dispatch(
            setStartEndValidation(
              "hBenefitesCostValid",
              "Health benefits cost should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.netBillRate)) {
          dispatch(
            setStartEndValidation(
              "netBillRateValid",
              "Net bill rate should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.netPurchase)) {
          dispatch(
            setStartEndValidation(
              "netPurchaseValid",
              "Net purchase should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.margin)) {
          dispatch(
            setStartEndValidation("marginValid", "Margin should not be empty.")
          );
        }
        if (isTextValid(currentStartEndOperationsData.fullTimeSalaryOffered)) {
          dispatch(
            setStartEndValidation(
              "fullTimeSalaryOfferedValid",
              "Full time salary offered should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.joiningStatus?.value)) {
          dispatch(
            setStartEndValidation(
              "joiningStatusValid",
              "Joining status should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.joiningType?.value)) {
          dispatch(
            setStartEndValidation(
              "joiningTypeValid",
              "Joining type should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.exitClearance?.value)) {
          dispatch(
            setStartEndValidation(
              "exitClearanceValid",
              "Exit clearance type should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.endReason?.value)) {
          dispatch(
            setStartEndValidation(
              "endReasonValid",
              "End reason type should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.jobLevel?.value)) {
          dispatch(
            setStartEndValidation(
              "jobLevelValid",
              "Job levelshould not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.ffInvoiceStatus)) {
          dispatch(
            setStartEndValidation(
              "ffInvoiceStatusValid",
              "Select FF invoice status should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.ffInvoiceStatus)) {
          dispatch(
            setStartEndValidation(
              "joiningStatusRemarkValid",
              "Joining status remarks should not be empty."
            )
          );
        }
        if (isTextValid(currentStartEndOperationsData.endRemarks)) {
          dispatch(
            setStartEndValidation(
              "endRemarksValid",
              "End remarks should not be empty."
            )
          );
        }

        if (
          validationStartEndOperationsData?.recruiterValid === " " &&
          validationStartEndOperationsData?.teamLeadValid === " " &&
          validationStartEndOperationsData?.teamManagerValid === " " &&
          validationStartEndOperationsData?.seniorManagerValid === " " &&
          validationStartEndOperationsData?.assoDirectorValid === " " &&
          validationStartEndOperationsData?.centerHeadValid === " " &&
          validationStartEndOperationsData?.onsiteAccDirectorValid === " " &&
          validationStartEndOperationsData?.onboCoordinatorValid === " " &&
          validationStartEndOperationsData?.endDateValid === " " &&
          validationStartEndOperationsData?.grossBrValid === " " &&
          validationStartEndOperationsData?.mspFeePercentageValid === " " &&
          validationStartEndOperationsData?.refFeeValid === " " &&
          validationStartEndOperationsData?.taxOHPercentageValid === " " &&
          validationStartEndOperationsData?.hBenefitesOptedValid === " " &&
          validationStartEndOperationsData?.hBenefitesCostValid === " " &&
          validationStartEndOperationsData?.netBillRateValid === " " &&
          validationStartEndOperationsData?.netPurchaseValid === " " &&
          validationStartEndOperationsData?.fullTimeSalaryOfferedValid ===
            " " &&
          validationStartEndOperationsData?.joiningStatusValid === " " &&
          validationStartEndOperationsData?.joiningTypeValid === " " &&
          validationStartEndOperationsData?.exitClearanceValid === " " &&
          validationStartEndOperationsData?.endReasonValid === " " &&
          validationStartEndOperationsData?.jobLevelValid === " "
        ) {
          setStepCount(stepCount + 1);
        }
      }
