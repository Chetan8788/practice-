import * as React from "react";
import Backdrop from "@mui/material/Backdrop";
import Box from "@mui/material/Box";
// import Modal from '@mui/material/Modal';
// import Button from '@mui/material/Button';
import Typography from "@mui/material/Typography";
import { useSpring, animated } from "@react-spring/web";
import CloseIcon from "@mui/icons-material/Close";
import EditIcon from "@mui/icons-material/Edit";
import DoneIcon from "@mui/icons-material/Done";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import {
  ArticlesOfIncorporationList,
  CertificateOfInsuranceList,
  CipcicaCipcicuList,
  ClientTaskOrderOrSOWList,
  ClientTaskOrderOrSOWStepList,
  ClientTaskOrderSigningList,
  DirectDepositeAgreementList,
  DocumentationStatusList,
  EVerifyList,
  EemergencyFormList,
  GoodStandingDocumentationList,
  I9FormList,
  ListADocumentsList,
  ListBDocumentsList,
  ListCDocumentsList,
  MSAList,
  SOWList,
  VaccinationStatusList,
  VoidCheckEmailList,
  W9W4List,
  WorkAuthorizeDocumentationList,
} from "../../constants/constants";
import Select from "react-select";
import { Modal } from "../../common/Modal/Modal";
import { DropDown } from "../../common/DropDown/DropDown";
import { DatePicker } from "../../common/DatePicker/DatePicker";
import moment from "moment";
import { Button } from "../../common/Button/Button";
import { editCandidateDocumentationData } from "../../actions/documentation";
import { RootState } from "../../redux/store";
import { Grid } from "@mui/material";
import { useEffect, useState } from "react";
import { isTextValid } from "../../helpers/validate";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";

interface FadeProps {
  children: React.ReactElement;
  in?: boolean;
  onClick?: any;
  onEnter?: (node: HTMLElement, isAppearing: boolean) => void;
  onExited?: (node: HTMLElement, isAppearing: boolean) => void;
  ownerState?: any;
}

const Fade = React.forwardRef<HTMLDivElement, FadeProps>(function Fade(
  props,
  ref
) {
  const {
    children,
    in: open,
    onClick,
    onEnter,
    onExited,
    ownerState,
    ...other
  } = props;
  const style = useSpring({
    from: { opacity: 0 },
    to: { opacity: open ? 1 : 0 },
    onStart: () => {
      if (open && onEnter) {
        onEnter(null as any, true);
      }
    },
    onRest: () => {
      if (!open && onExited) {
        onExited(null as any, true);
      }
    },
  });

  return (
    <animated.div ref={ref} style={style} {...other}>
      {React.cloneElement(children, { onClick })}
    </animated.div>
  );
});

const style = {
  position: "absolute" as "absolute",
  top: "50%",
  left: "50%",
  transform: "translate(-50%, -50%)",
  width: 400,
  bgcolor: "background.paper",
  border: "1px #000",
  boxShadow: 24,
  p: 4,
  borderRadius: "10px",
};

interface Props {
  open: any;
  setOpen: any;
  data: any;
  showTableCount: any;
  int: any;
  setShowModal: any;
}

const ShowDocumentation: React.FC<Props> = ({
  open,
  setOpen,
  // data,
  showTableCount,
  int,
  setShowModal,
}) => {
  const dispatch = useAppDispatch();
  let data = useAppSelector(
    (state: RootState) => state?.documentation?.singleDocumentationData
  );
  const [disable, setDisable] = React.useState(true);

  const [
    articlesOrCertificateOFIncorporation,
    setArticlesOrCertificateOFIncorporation,
  ] = React.useState({
    value: data?.articlesOrCertificateOFIncorporation,
    label: data?.articlesOrCertificateOFIncorporation,
  });

  const [w9Orw4, setW9Orw4] = React.useState({
    value: data?.w9Orw4,
    label: data?.w9Orw4,
  });
  const [directDepositAgreement, setDirectDepositAgreement] = React.useState({
    value: data?.directDepositAgreement,
    label: data?.directDepositAgreement,
  });
  const [voidCheckOrEmailContent, setVoidCheckOrEmailContent] = React.useState({
    value: data?.voidCheckOrEmailContent,
    label: data?.voidCheckOrEmailContent,
  });
  const [CIPCICICAOrCIPCICU, setCIPCICICAOrCIPCICU] = React.useState({
    value: data?.CIPCICICAOrCIPCICU,
    label: data?.CIPCICICAOrCIPCICU,
  });
  const [goodStandingDocument, setGoodStandingDocument] = React.useState({
    value: data?.goodStandingDocument,
    label: data?.goodStandingDocument,
  });
  const [workAuthorizationDocument, setWorkAuthorizationDocument] =
    React.useState({
      value: data?.workAuthorizationDocument,
      label: data?.workAuthorizationDocument,
    });
  const [I9Form, setI9Form] = React.useState({
    value: data?.I9Form,
    label: data?.I9Form,
  });
  const [listADocument, setListADocument] = React.useState({
    value: data?.listADocument,
    label: data?.listADocument,
  });
  const [listBDocument, setListBDocument] = React.useState({
    value: data?.listBDocument,
    label: data?.listBDocument,
  });
  const [listCDocument, setListCDocument] = React.useState({
    value: data?.listCDocument,
    label: data?.listCDocument,
  });
  const [E_verify, setE_verify] = React.useState({
    value: data?.E_verify,
    label: data?.E_verify,
  });
  const [E_verificationDate, setE_verificationDate] = React.useState(
    moment.utc(data?.E_verificationDate).format("YYYY-MM-DD")
  );
  const [emergencyForm, setEmergencyForm] = React.useState({
    value: data?.emergencyForm,
    label: data?.emergencyForm,
  });
  const [vaccinationStatus, setVaccinationStatus] = React.useState({
    value: data?.vaccinationStatus,
    label: data?.vaccinationStatus,
  });
  const [clientTaskOrderOrSOWst, setClientTaskOrderOrSOWst] = React.useState({
    value: data?.clientTaskOrderOrSOWst,
    label: data?.clientTaskOrderOrSOWst,
  });
  const [MSA, setMSA] = React.useState({
    value: data?.MSA,
    label: data?.MSA,
  });
  const [SOW, setSOW] = React.useState({
    value: data?.SOW,
    label: data?.SOW,
  });
  const [SOWValidity, setSOWValidity] = React.useState(
    moment.utc(data?.SOWValidity).format("YYYY-MM-DD")
  );
  const [certificateOFInsuranceOrCOI, setCertificateOFInsuranceOrCOI] =
    React.useState({
      value: data?.certificateOFInsuranceOrCOI,
      label: data?.certificateOFInsuranceOrCOI,
    });
  const [clientTaskOrderSigning, setClientTaskOrderSigning] = React.useState({
    value: data?.certificateOFInsuranceOrCOI,
    label: data?.certificateOFInsuranceOrCOI,
  });
  const [TaskOrderExpiryDate, setTaskOrderExpiryDate] = React.useState(
    moment.utc(data?.TaskOrderExpiryDate).format("YYYY-MM-DD")
  );
  const [certificationOfInsurance, setCertificationOfInsurance] =
    React.useState(
      moment.utc(data?.certificationOfInsurance).format("YYYY-MM-DD")
    );
  const [clientTaskOrderOrSOW, setClientTaskOrderOrSOW] = React.useState({
    value: data?.clientTaskOrderOrSOW,
    label: data?.clientTaskOrderOrSOW,
  });
  const [documentationStatus, setDocumentationStatus] = React.useState({
    value: data?.documentationStatus,
    label: data?.documentationStatus,
  });
  const [documentationCompletionDate, setDocumentationCompletionDate] =
    React.useState(
      moment.utc(data?.documentationCompletionDate).format("YYYY-MM-DD")
    );
  const [documentationRemark, setDocumentationRemark] = React.useState(
    data?.documentationRemark
  );
  const [count, setCount] = React.useState(0);

  React.useEffect(() => {
    setArticlesOrCertificateOFIncorporation({
      value: data?.articlesOrCertificateOFIncorporation,
      label: data?.articlesOrCertificateOFIncorporation,
    });
    setW9Orw4({
      value: data?.w9Orw4,
      label: data?.w9Orw4,
    });
    setDirectDepositAgreement({
      value: data?.directDepositAgreement,
      label: data?.directDepositAgreement,
    });
    setVoidCheckOrEmailContent({
      value: data?.voidCheckOrEmailContent,
      label: data?.voidCheckOrEmailContent,
    });
    setCIPCICICAOrCIPCICU({
      value: data?.CIPCICICAOrCIPCICU,
      label: data?.CIPCICICAOrCIPCICU,
    });
    setGoodStandingDocument({
      value: data?.goodStandingDocument,
      label: data?.goodStandingDocument,
    });
    setWorkAuthorizationDocument({
      value: data?.workAuthorizationDocument,
      label: data?.workAuthorizationDocument,
    });
    setI9Form({
      value: data?.I9Form,
      label: data?.I9Form,
    });
    setListADocument({
      value: data?.listADocument,
      label: data?.listADocument,
    });
    setListBDocument({
      value: data?.listBDocument,
      label: data?.listBDocument,
    });
    setListCDocument({
      value: data?.listCDocument,
      label: data?.listCDocument,
    });
    setE_verify({
      value: data?.E_verify,
      label: data?.E_verify,
    });
    setE_verificationDate(
      moment.utc(data?.E_verificationDate).format("YYYY-MM-DD")
    );
    setEmergencyForm({
      value: data?.emergencyForm,
      label: data?.emergencyForm,
    });
    setVaccinationStatus({
      value: data?.vaccinationStatus,
      label: data?.vaccinationStatus,
    });
    setClientTaskOrderOrSOWst({
      value: data?.clientTaskOrderOrSOWst,
      label: data?.clientTaskOrderOrSOWst,
    });
    setMSA({
      value: data?.MSA,
      label: data?.MSA,
    });
    setSOW({
      value: data?.SOW,
      label: data?.SOW,
    });
    setSOWValidity(moment.utc(data?.SOWValidity).format("YYYY-MM-DD"));
    setCertificateOFInsuranceOrCOI({
      value: data?.certificateOFInsuranceOrCOI,
      label: data?.certificateOFInsuranceOrCOI,
    });
    setClientTaskOrderSigning({
      value: data?.certificateOFInsuranceOrCOI,
      label: data?.certificateOFInsuranceOrCOI,
    });
    setTaskOrderExpiryDate(
      moment.utc(data?.TaskOrderExpiryDate).format("YYYY-MM-DD")
    );
    setCertificationOfInsurance(
      moment.utc(data?.certificationOfInsurance).format("YYYY-MM-DD")
    );
    setClientTaskOrderOrSOW({
      value: data?.clientTaskOrderOrSOW,
      label: data?.clientTaskOrderOrSOW,
    });
    setDocumentationStatus({
      value: data?.documentationStatus,
      label: data?.documentationStatus,
    });
    setDocumentationCompletionDate(
      moment.utc(data?.documentationCompletionDate).format("YYYY-MM-DD")
    );
    setDocumentationRemark(data?.documentationRemark);
    setCount(1);
  }, [data]);

  const [
    articlesOrCertificateOFIncorporationValid,
    setArticlesOrCertificateOFIncorporationValid,
  ] = useState<boolean>();

  const [w9Orw4Valid, setW9Orw4Valid] = useState<boolean>();
  const [directDepositAgreementValid, setDirectDepositAgreementValid] =
    useState<boolean>();
  const [voidCheckOrEmailContentValid, setVoidCheckOrEmailContentValid] =
    useState<boolean>();
  const [CIPCICICAOrCIPCICUValid, setCIPCICICAORCIPCICUValid] =
    useState<boolean>();
  const [goodStandingDocumentValid, setGoodStandingDocumentValid] =
    useState<boolean>();
  const [workAuthorizationDocumentValid, setWorkAuthorizationDocumentValid] =
    useState<boolean>();
  const [I9FormValid, setI9FOrmValid] = useState<boolean>();
  const [listADocumentValid, setListADocumentValid] = useState<boolean>();
  const [listBDocumentValid, setListBDocumentValid] = useState<boolean>();
  const [listCDocumentValid, setListCDocumentValid] = useState<boolean>();
  const [E_verifyValid, setE_VerifyValid] = useState<boolean>();
  const [E_verificationDateValid, setE_VerificationDateValid] =
    useState<boolean>();
  const [emergencyFormValid, setemergencyFormValid] = useState<boolean>();
  const [vaccinationStatusValid, setVaccinationStatusValid] =
    useState<boolean>();
  const [clientTaskOrderOrSOWstValid, setClientTaskOrderOrSOWstValid] =
    useState<boolean>();
  const [MSAValid, setMSAValid] = useState<boolean>();
  const [SOWValid, setSOWValid] = useState<boolean>();
  const [SOWValidityValid, setSOWVAlidityValid] = useState<boolean>();
  const [
    certificateOFInsuranceOrCOIValid,
    setCertificateOFInsuranceOrCOIValid,
  ] = useState<boolean>();
  const [clientTaskOrderSigningValid, setClientTaskOrderSigningValid] =
    useState<boolean>();
  const [TaskOrderExpiryDateValid, setTAskOrderExpiryDateValid] =
    useState<boolean>();
  const [certificationOfInsuranceValid, setCertificationOfInsuranceValid] =
    useState<boolean>();

  const [documentationStatusValid, setDocumentationStatusValid] =
    useState<boolean>();
  const [clientTaskOrderOrSOWValid, setClientTaskOrderOrSOWValid] =
    useState<boolean>();
  const [documentationRemarkValid, setDocumentationRemarkValid] =
    useState<boolean>();
  const [
    documentationCompletionDateValid,
    setDocumentationCompletionDateValid,
  ] = useState<boolean>();

  const [
    articlesOrCertificateOFIncorporationError,
    setArticlesOrCertificateOFIncorporationError,
  ] = useState<any>();

  const [w9Orw4Error, setW9Orw4Error] = useState<any>();
  const [directDepositAgreementError, setDirectDepositAgreementError] =
    useState<any>();
  const [voidCheckOrEmailContentError, setVoidCheckOrEmailContentError] =
    useState<any>();
  const [CIPCICICAOrCIPCICUError, setCIPCICICAORCIPCICUError] = useState<any>();
  const [goodStandingDocumentError, setGoodStandingDocumentError] =
    useState<any>();
  const [workAuthorizationDocumentError, setWorkAuthorizationDocumentError] =
    useState<any>();
  const [I9FormError, setI9FOrmError] = useState<any>();
  const [listADocumentError, setListADocumentError] = useState<any>();
  const [listBDocumentError, setListBDocumentError] = useState<any>();
  const [listCDocumentError, setListCDocumentError] = useState<any>();
  const [E_verifyError, setE_VerifyError] = useState<any>();
  const [E_verificationDateError, setE_VerificationDateError] = useState<any>();
  const [emergencyFormError, setemergencyFormError] = useState<any>();
  const [vaccinationStatusError, setVaccinationStatusError] = useState<any>();
  const [clientTaskOrderOrSOWstError, setClientTaskOrderOrSOWstError] =
    useState<any>();
  const [MSAError, setMSAError] = useState<any>();
  const [SOWError, setSOWError] = useState<any>();
  const [SOWValidityError, setSOWVAlidityError] = useState<any>();
  const [
    certificateOFInsuranceOrCOIError,
    setCertificateOFInsuranceOrCOIError,
  ] = useState<any>();
  const [clientTaskOrderSigningError, setClientTaskOrderSigningError] =
    useState<any>();
  const [TaskOrderExpiryDateError, setTAskOrderExpiryDateError] =
    useState<any>();
  const [certificationOfInsuranceError, setCertificationOfInsuranceError] =
    useState<any>();

  const [documentationStatusError, setDocumentationStatusError] =
    useState<any>();
  const [clientTaskOrderOrSOWError, setClientTaskOrderOrSOWError] =
    useState<any>();
  const [documentationRemarkError, setDocumentationRemarkError] =
    useState<any>();
  const [
    documentationCompletionDateError,
    setDocumentationCompletionDateError,
  ] = useState<any>();

  function updateCandidateDocumentation() {
    setArticlesOrCertificateOFIncorporationValid(
      isTextValid(articlesOrCertificateOFIncorporation.value)
    );
    setW9Orw4Valid(isTextValid(w9Orw4.value));
    setDirectDepositAgreementValid(isTextValid(directDepositAgreement.value));
    setVoidCheckOrEmailContentValid(isTextValid(voidCheckOrEmailContent.value));
    setCIPCICICAORCIPCICUValid(isTextValid(CIPCICICAOrCIPCICU.value));
    setGoodStandingDocumentValid(isTextValid(goodStandingDocument.value));
    setWorkAuthorizationDocumentValid(
      isTextValid(workAuthorizationDocument.value)
    );
    setI9FOrmValid(isTextValid(I9Form.value));
    setListADocumentValid(isTextValid(listADocument.value));
    setListBDocumentValid(isTextValid(listBDocument.value));
    setListCDocumentValid(isTextValid(listCDocument.value));
    setE_VerifyValid(isTextValid(E_verify.value));
    setE_VerificationDateValid(isTextValid(E_verificationDate));
    setemergencyFormValid(isTextValid(emergencyForm.value));
    setVaccinationStatusValid(isTextValid(vaccinationStatus.value));
    setClientTaskOrderOrSOWstValid(isTextValid(clientTaskOrderOrSOWst.value));

    setMSAValid(isTextValid(MSA.value));
    setSOWValid(isTextValid(SOW.value));
    setSOWVAlidityValid(isTextValid(SOWValidity));
    setCertificateOFInsuranceOrCOIValid(
      isTextValid(certificateOFInsuranceOrCOI.value)
    );
    setClientTaskOrderSigningValid(isTextValid(clientTaskOrderSigning.value));
    setTAskOrderExpiryDateValid(isTextValid(TaskOrderExpiryDate));
    setCertificationOfInsuranceValid(isTextValid(certificationOfInsurance));
    setClientTaskOrderOrSOWValid(isTextValid(clientTaskOrderOrSOW.value));
    setDocumentationStatusValid(isTextValid(documentationStatus.value));
    setDocumentationCompletionDateValid(
      isTextValid(documentationCompletionDate)
    );
    setDocumentationRemarkValid(isTextValid(documentationRemark));

    if (
      articlesOrCertificateOFIncorporationValid &&
      w9Orw4Valid &&
      directDepositAgreementValid &&
      voidCheckOrEmailContentValid &&
      CIPCICICAOrCIPCICUValid &&
      goodStandingDocumentValid &&
      workAuthorizationDocumentValid &&
      I9FormValid &&
      listADocumentValid &&
      listBDocumentValid &&
      listCDocumentValid &&
      E_verifyValid &&
      E_verificationDateValid &&
      emergencyFormValid &&
      vaccinationStatusValid &&
      clientTaskOrderOrSOWstValid &&
      MSAValid &&
      SOWValid &&
      SOWValidityValid &&
      certificateOFInsuranceOrCOIValid &&
      clientTaskOrderSigningValid &&
      TaskOrderExpiryDateValid &&
      certificationOfInsuranceValid &&
      documentationStatusValid &&
      clientTaskOrderOrSOWValid &&
      documentationRemarkValid &&
      documentationCompletionDateValid
    ) {
      dispatch(
        editCandidateDocumentationData(
          articlesOrCertificateOFIncorporation,
          w9Orw4,
          directDepositAgreement,
          voidCheckOrEmailContent,
          CIPCICICAOrCIPCICU,
          goodStandingDocument,
          workAuthorizationDocument,
          I9Form,
          listADocument,
          listBDocument,
          listCDocument,
          E_verify,
          E_verificationDate,
          emergencyForm,
          vaccinationStatus,
          clientTaskOrderOrSOWst,
          MSA,
          SOW,
          SOWValidity,
          certificateOFInsuranceOrCOI,
          clientTaskOrderSigning,
          TaskOrderExpiryDate,
          certificationOfInsurance,
          clientTaskOrderOrSOW,
          documentationStatus,
          documentationCompletionDate,
          documentationRemark,

          data?.candidateId
        )
      );
      setShowModal(false);
    } else {
      if (!articlesOrCertificateOFIncorporationValid) {
        setArticlesOrCertificateOFIncorporationError(
          "articles Or Certificat eOF Incorporation should not be empty."
        );
      }
      if (!w9Orw4Valid) {
        setW9Orw4Error("w9Orw4 should not be empty.");
      }
      if (!directDepositAgreementValid) {
        setDirectDepositAgreementError(
          "direct Deposit Agreement should not be empty."
        );
      }

      if (!voidCheckOrEmailContentValid) {
        setVoidCheckOrEmailContentError(
          "void Check Or Email Content should not be empty."
        );
      }
      if (!CIPCICICAOrCIPCICUValid) {
        setCIPCICICAORCIPCICUError("CIPCICICA Or CIPCICU should not be empty.");
      }
      if (!goodStandingDocumentValid) {
        setGoodStandingDocumentError(
          "good Standing Document should not be empty."
        );
      }
      if (!workAuthorizationDocumentValid) {
        setWorkAuthorizationDocumentError(
          "workAuthorization Document should not be empty."
        );
      }
      if (!I9FormValid) {
        setI9FOrmError("I9 Form should not be empty.");
      }
      if (!listADocumentValid) {
        setListADocumentError("listA Document should not be empty.");
      }
      if (!listBDocumentValid) {
        setListBDocumentError("listB Document should not be empty.");
      }
      if (!listCDocumentValid) {
        setListCDocumentError("listC DocumentValid should not be empty.");
      }
      if (!E_verifyValid) {
        setE_VerifyError("E_verify should not be empty.");
      }
      if (!E_verificationDateValid) {
        setE_VerificationDateError("E_verification Date should not be empty.");
      }
      if (!emergencyFormValid) {
        setemergencyFormError("emergency Form should not be empty.");
      }
      if (!vaccinationStatusValid) {
        setVaccinationStatusError("vaccination Status should not be empty.");
      }
      if (!clientTaskOrderOrSOWstValid) {
        setClientTaskOrderOrSOWError(
          "client Task Order Or SOWst should not be empty."
        );
      }
      if (!MSAValid) {
        setMSAError("MSA should not be empty.");
      }
      if (!SOWValid) {
        setSOWError("SOW should not be empty.");
      }
      if (!SOWValidityValid) {
        setSOWVAlidityError("SOW Validity should not be empty.");
      }
      if (!certificateOFInsuranceOrCOIValid) {
        setCertificateOFInsuranceOrCOIError(
          "certificate OF Insurance Or COI should not be empty."
        );
      }
      if (!clientTaskOrderSigningValid) {
        setClientTaskOrderSigningError(
          "client Task Order Signing should not be empty."
        );
      }
      if (!TaskOrderExpiryDateValid) {
        setTAskOrderExpiryDateError(
          "Task Order Expiry Date should not be empty."
        );
      }
      if (!certificationOfInsuranceValid) {
        setCertificationOfInsuranceError(
          "certification Of Insurance should not be empty."
        );
      }
      if (!documentationStatusValid) {
        setDocumentationStatusError(
          "documentation Status should not be empty."
        );
      }
      if (!clientTaskOrderOrSOWValid) {
        setClientTaskOrderOrSOWError(
          "client Task OrderOrSOW should not be empty."
        );
      }
      if (!documentationRemarkValid) {
        setDocumentationRemarkError(
          "documentation Remark should not be empty."
        );
      }
      if (!documentationCompletionDateValid) {
        setDocumentationCompletionDateError(
          "documentation Completion Date should not be empty."
        );
      }
    }
  }

  return (
    <div className="pt-10 pl-10 h-[60vh] overflow-auto" id="no-scroll-div">
      <Grid container spacing={2} columnGap={"15px"}>
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={CIPCICICAOrCIPCICU}
            options={CipcicaCipcicuList}
            onChange={(e: any) => {
              setCIPCICICAOrCIPCICU(e);
              setCIPCICICAORCIPCICUValid(isTextValid(e?.value));
              if (!CIPCICICAOrCIPCICUValid) {
                setCIPCICICAORCIPCICUError(
                  "CIPCICICAORCIPCICUE should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!CIPCICICAOrCIPCICUValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {CIPCICICAOrCIPCICUError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">E-verification Date</td>
          <td className="px-6 py-4">
            <FloatLabel
              value={E_verificationDate}
              type="date"
              handleChange={(e: any) => {
                setE_verificationDate(e.target.value);
              }}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="E_verificationDate"
            type="date"
            value={E_verificationDate}
            placeholder={""}
            handleChange={(event) => {
              setE_verificationDate(event.target.value);
              setE_VerificationDateValid(isTextValid(event.target.value));
              if (!E_verificationDateValid) {
                setE_VerificationDateError(
                  "E-verification Date should not be empty."
                );
              }
            }}
            className=""
          />
          {!E_verificationDateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {E_verificationDateError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">E-verify</td>
          <td className="px-6 py-4">
            <Select
              value={E_verify}
              options={EVerifyList}
              onChange={(e: any) => setE_verify(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={E_verify}
            options={EVerifyList}
            onChange={(e: any) => {
              setE_verify(e);
              setE_VerifyValid(isTextValid(e?.value));
              if (!E_verifyValid) {
                setE_VerifyError("E-verify should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!E_verifyValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "10px" }}
            >
              {E_verifyError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">I9 form</td>
          <td className="px-6 py-4">
            <Select
              value={I9Form}
              options={I9FormList}
              onChange={(e: any) => setI9Form(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={I9Form}
            options={I9FormList}
            onChange={(e: any) => {
              setI9Form(e);
              setI9FOrmValid(isTextValid(e?.value));
              if (!I9FormValid) {
                setI9FOrmError("I9 form should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!I9FormValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "10px" }}
            >
              {I9FormError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">MSA</td>
          <td className="px-6 py-4">
            <Select
              value={MSA}
              options={MSAList}
              onChange={(e: any) => setMSA(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={MSA}
            options={MSAList}
            onChange={(e: any) => {
              setMSA(e);
              setMSAValid(isTextValid(e?.value));
              if (!MSAValid) {
                setMSAError("MSA should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!MSAValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {MSAError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">SOW</td>
          <td className="px-6 py-4">
            <Select
              value={SOW}
              options={SOWList}
              onChange={(e: any) => setSOW(e)}
            />
          </td>
        </tr> */}{" "}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={SOW}
            options={SOWList}
            onChange={(e: any) => {
              setSOW(e);
              setSOWValid(isTextValid(e?.value));
              if (!SOWValid) {
                setSOWError("SOW should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!SOWValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {SOWError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">SOW validity</td>
          <td className="px-6 py-4">
            <TextField
              value={SOWValidity}
              type="date"
              handleChange={(e: any) => {
                setSOWValidity(e.target.value);
              }}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="SOW validity"
            type="date"
            value={SOWValidity}
            placeholder={""}
            handleChange={(event) => {
              setSOWValidity(event.target.value);
              setSOWVAlidityValid(isTextValid(event.target.value));
              if (!SOWValidityValid) {
                setSOWVAlidityError("SOW validity should not be empty.");
              }
            }}
            className=""
          />
          {!SOWValidityValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "10px" }}
            >
              {SOWValidityError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Task order expiry date</td>
          <td className="px-6 py-4">
            <TextField
              value={TaskOrderExpiryDate}
              type="date"
              handleChange={(e: any) => {
                setTaskOrderExpiryDate(e.target.value);
              }}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Task order expiry date"
            type="date"
            value={TaskOrderExpiryDate}
            placeholder={""}
            handleChange={(event) => {
              setTaskOrderExpiryDate(event.target.value);
              setTAskOrderExpiryDateValid(isTextValid(event.target.value));
              if (!TaskOrderExpiryDateValid) {
                setTAskOrderExpiryDateError(
                  "Task order expiry date should not be empty."
                );
              }
            }}
            className=""
          />
          {!TaskOrderExpiryDateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "10px" }}
            >
              {TaskOrderExpiryDateError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">
            Articles or certificate of incorporation
          </td>
          <td className="px-6 py-4">
            <Select
              value={articlesOrCertificateOFIncorporation}
              options={ArticlesOfIncorporationList}
              onChange={(e: any) => setArticlesOrCertificateOFIncorporation(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={articlesOrCertificateOFIncorporation}
            options={ArticlesOfIncorporationList}
            onChange={(e: any) => {
              setArticlesOrCertificateOFIncorporation(e);
              setArticlesOrCertificateOFIncorporationValid(
                isTextValid(e?.value)
              );
              if (!articlesOrCertificateOFIncorporationValid) {
                setArticlesOrCertificateOFIncorporationError(
                  "Articles or certificate of incorporation should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!articlesOrCertificateOFIncorporationValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {articlesOrCertificateOFIncorporationError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Certificate of insurance or COI</td>
          <td className="px-6 py-4">
            <Select
              value={certificateOFInsuranceOrCOI}
              options={CertificateOfInsuranceList}
              onChange={(e: any) => setCertificateOFInsuranceOrCOI(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={certificateOFInsuranceOrCOI}
            options={CertificateOfInsuranceList}
            onChange={(e: any) => {
              setCertificateOFInsuranceOrCOI(e);
              setCertificateOFInsuranceOrCOIValid(isTextValid(e?.value));
              if (!certificateOFInsuranceOrCOIValid) {
                setCertificateOFInsuranceOrCOIError(
                  "Certificate of insurance or COI should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!certificateOFInsuranceOrCOIValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {certificateOFInsuranceOrCOIError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Certificate of insurance Date</td>
          <td className="px-6 py-4">
            <TextField
              value={certificationOfInsurance}
              type="date"
              handleChange={(e: any) => {
                setCertificationOfInsurance(e.target.value);
              }}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Certificate of insurance Date"
            type="date"
            value={certificationOfInsurance}
            placeholder={""}
            handleChange={(event) => {
              setCertificationOfInsurance(event.target.value);
              setCertificationOfInsuranceValid(isTextValid(event.target.value));
              if (!certificationOfInsuranceValid) {
                setCertificationOfInsuranceError(
                  "Certificate of insurance Date should not be empty."
                );
              }
            }}
            className=""
          />
          {!certificationOfInsuranceValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {certificationOfInsuranceError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Client task order or sow</td>
          <td className="px-6 py-4">
            <Select
              value={clientTaskOrderOrSOW}
              options={ClientTaskOrderOrSOWList}
              onChange={(e: any) => setClientTaskOrderOrSOW(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={clientTaskOrderOrSOW}
            options={ClientTaskOrderOrSOWList}
            onChange={(e: any) => {
              setClientTaskOrderOrSOW(e);
              setClientTaskOrderOrSOWValid(isTextValid(e?.value));
              if (!clientTaskOrderOrSOWValid) {
                setClientTaskOrderOrSOWError(
                  "Client task order or sow should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!clientTaskOrderOrSOWValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {clientTaskOrderOrSOWError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Client task order or sow st</td>
          <td className="px-6 py-4">
            <Select
              value={clientTaskOrderOrSOWst}
              options={ClientTaskOrderOrSOWStepList}
              onChange={(e: any) => setClientTaskOrderOrSOWst(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={clientTaskOrderOrSOWst}
            options={ClientTaskOrderOrSOWStepList}
            onChange={(e: any) => {
              setClientTaskOrderOrSOWst(e);
              setClientTaskOrderOrSOWstValid(isTextValid(e?.value));
              if (!clientTaskOrderOrSOWstValid) {
                setClientTaskOrderOrSOWstError(
                  "Client task order or sow st should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!clientTaskOrderOrSOWstValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {clientTaskOrderOrSOWstError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Client task order signing</td>
          <td className="px-6 py-4">
            {data?.docData?.clientTaskOrderSigning}
            <Select
              value={clientTaskOrderSigning}
              options={ClientTaskOrderSigningList}
              onChange={(e: any) => setClientTaskOrderSigning(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={clientTaskOrderSigning}
            options={ClientTaskOrderSigningList}
            onChange={(e: any) => {
              setClientTaskOrderSigning(e);
              setClientTaskOrderSigningValid(isTextValid(e?.value));
              if (!clientTaskOrderSigningValid) {
                setClientTaskOrderSigningError(
                  "Client task order signing should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!clientTaskOrderSigningValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {clientTaskOrderSigningError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Direct deposit agreement</td>
          <td className="px-6 py-4">
            <Select
              value={directDepositAgreement}
              options={DirectDepositeAgreementList}
              onChange={(e: any) => setDirectDepositAgreement(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={directDepositAgreement}
            options={DirectDepositeAgreementList}
            onChange={(e: any) => {
              setDirectDepositAgreement(e);
              setDirectDepositAgreementValid(isTextValid(e?.value));
              if (!directDepositAgreementValid) {
                setDirectDepositAgreementError(
                  "Direct deposit agreement should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!directDepositAgreementValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {directDepositAgreementError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Documentation completion date</td>
          <td className="px-6 py-4">
            <TextField
              value={documentationCompletionDate}
              type="date"
              handleChange={(e: any) => {
                setDocumentationCompletionDate(e.target.value);
              }}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Documentation completion date"
            type="date"
            value={documentationCompletionDate}
            placeholder={""}
            handleChange={(event) => {
              setDocumentationCompletionDate(event.target.value);
              setDocumentationCompletionDateValid(
                isTextValid(event.target.value)
              );
              if (!documentationCompletionDateValid) {
                setDocumentationCompletionDateError(
                  "Documentation completion date should not be empty."
                );
              }
            }}
            className=""
          />
          {!documentationCompletionDateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {documentationCompletionDateError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Documentation status</td>
          <td className="px-6 py-4">
            {data?.docData?.documentationStatus}
            <Select
              value={documentationStatus}
              options={DocumentationStatusList}
              onChange={(e: any) => setDocumentationStatus(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={documentationStatus}
            options={DocumentationStatusList}
            onChange={(e: any) => {
              setDocumentationStatus(e);
              setDocumentationStatusValid(isTextValid(e?.value));
              if (!documentationStatusValid) {
                setDocumentationStatusError(
                  "Documentation status should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!documentationStatusValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {documentationStatusError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Emergency form</td>
          <td className="px-6 py-4">
            <Select
              value={emergencyForm}
              options={EemergencyFormList}
              onChange={(e: any) => setEmergencyForm(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={emergencyForm}
            options={EemergencyFormList}
            onChange={(e: any) => {
              setEmergencyForm(e);
              setemergencyFormValid(isTextValid(e?.value));
              if (!emergencyFormValid) {
                setemergencyFormError("Emergency form should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!emergencyFormValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {emergencyFormError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Good standing document</td>
          <td className="px-6 py-4">
            {data?.docData?.goodStandingDocument}
            <Select
              value={goodStandingDocument}
              options={GoodStandingDocumentationList}
              onChange={(e: any) => setGoodStandingDocument(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={goodStandingDocument}
            options={GoodStandingDocumentationList}
            onChange={(e: any) => {
              setGoodStandingDocument(e);
              setGoodStandingDocumentValid(isTextValid(e?.value));
              if (!goodStandingDocumentValid) {
                setGoodStandingDocumentError(
                  "Good standing document should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!goodStandingDocumentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {goodStandingDocumentError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">List A document</td>
          <td className="px-6 py-4">
            <Select
              value={listADocument}
              options={ListADocumentsList}
              onChange={(e: any) => setListADocument(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={listADocument}
            options={ListADocumentsList}
            onChange={(e: any) => {
              setListADocument(e);
              setListADocumentValid(isTextValid(e?.value));
              if (!listADocumentValid) {
                setListADocumentError("List a document should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!listADocumentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {listADocumentError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">List B document</td>
          <td className="px-6 py-4">
            <Select
              value={listBDocument}
              options={ListBDocumentsList}
              onChange={(e: any) => setListBDocument(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={listBDocument}
            options={ListBDocumentsList}
            onChange={(e: any) => {
              setListBDocument(e);
              setListBDocumentValid(isTextValid(e?.value));
              if (!listBDocumentValid) {
                setListBDocumentError("List b document should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!listBDocumentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {listBDocumentError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">List C document</td>
          <td className="px-6 py-4">
            <Select
              value={listCDocument}
              options={ListCDocumentsList}
              onChange={(e: any) => setListCDocument(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={listCDocument}
            options={ListCDocumentsList}
            onChange={(e: any) => {
              setListCDocument(e);
              setListCDocumentValid(isTextValid(e?.value));
              if (!listCDocumentValid) {
                setListCDocumentError("List C documentshould not be empty");
              }
            }}
            isSearchable={true}
          />
          {!listCDocumentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {listCDocumentError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Vaccination status</td>
          <td className="px-6 py-4">
            <Select
              value={vaccinationStatus}
              options={VaccinationStatusList}
              onChange={(e: any) => setVaccinationStatus(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={vaccinationStatus}
            options={VaccinationStatusList}
            onChange={(e: any) => {
              setVaccinationStatus(e);
              setVaccinationStatusValid(isTextValid(e?.value));
              if (!vaccinationStatusValid) {
                setVaccinationStatusError(
                  "Vaccination status should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!vaccinationStatusValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {vaccinationStatusError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Void check or email content</td>
          <td className="px-6 py-4">
            <Select
              value={voidCheckOrEmailContent}
              options={VoidCheckEmailList}
              onChange={(e: any) => setVoidCheckOrEmailContent(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={voidCheckOrEmailContent}
            options={VoidCheckEmailList}
            onChange={(e: any) => {
              setVoidCheckOrEmailContent(e);
              setVoidCheckOrEmailContentValid(isTextValid(e?.value));
              if (!voidCheckOrEmailContentValid) {
                setVoidCheckOrEmailContentError(
                  "Void check or email content should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!voidCheckOrEmailContentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {voidCheckOrEmailContentError}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">W9 or W4</td>
          <td className="px-6 py-4">
            {data?.docData?.w9Orw4}
            <Select
              value={w9Orw4}
              options={W9W4List}
              onChange={(e: any) => setW9Orw4(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            className="text-[13px] text-left"
            value={w9Orw4}
            options={W9W4List}
            onChange={(e: any) => {
              setW9Orw4(e);
              setW9Orw4Valid(isTextValid(e?.value));
              if (!w9Orw4Valid) {
                setW9Orw4Error("W9 or W4 should not be empty");
              }
            }}
            isSearchable={true}
          />
          {!w9Orw4Valid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {w9Orw4Error}
            </p>
          ) : null}
        </Grid>
        {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-4">Work authorization document</td>
          <td className="px-6 py-4">
            {data?.docData?.workAuthorizationDocument}
            <Select
              value={workAuthorizationDocument}
              options={WorkAuthorizeDocumentationList}
              onChange={(e: any) => setWorkAuthorizationDocument(e)}
            />
          </td>
        </tr> */}
        <Grid xs={6} md={5.5}>
          <Select
            // aria-label="Work authorization document"
            // placeholder="Work authorization document"
            className="text-[13px] text-left"
            value={workAuthorizationDocument}
            options={WorkAuthorizeDocumentationList}
            onChange={(e: any) => {
              setWorkAuthorizationDocument(e);
              setWorkAuthorizationDocumentValid(isTextValid(e?.value));
              if (!workAuthorizationDocumentValid) {
                setWorkAuthorizationDocumentError(
                  "Work authorization document should not be empty"
                );
              }
            }}
            isSearchable={true}
          />
          {!workAuthorizationDocumentValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {workAuthorizationDocumentError}
            </p>
          ) : null}
        </Grid>
      </Grid>

      <div className="m-auto mb-3 w-[30%] ml-[30%] text-white">
        <Button
          className=""
          value="Update"
          handleClick={() => {
            updateCandidateDocumentation();
          }}
        />
      </div>
    </div>
  );
};

export default ShowDocumentation;
