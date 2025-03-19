# notre.diaporama
const CLIENT_ID = "TON_CLIENT_ID"; // Remplace par ton ID client
const API_KEY = "TA_CLÉ_API"; // Remplace par ta clé API
const SCOPES = "https://www.googleapis.com/auth/drive.readonly";

const handleFileSelect = async (index) => {
  await loadGooglePicker(index);
};

const loadGooglePicker = (index) => {
  gapi.load("client:auth2", async () => {
    await gapi.client.init({
      apiKey: API_KEY,
      clientId: CLIENT_ID,
      scope: SCOPES,
      discoveryDocs: ["https://www.googleapis.com/discovery/v1/apis/drive/v3/rest"],
    });

    gapi.auth2.getAuthInstance().signIn().then(() => {
      gapi.load("picker", () => {
        const picker = new google.picker.PickerBuilder()
          .addView(google.picker.ViewId.DOCS_IMAGES)
          .setOAuthToken(gapi.auth.getToken().access_token)
          .setCallback((data) => {
            if (data.action === google.picker.Action.PICKED) {
              const fileUrl = data.docs[0].url;
              const newPhotos = [...formData.photos];
              newPhotos[index].file = fileUrl;
              newPhotos[index].preview = fileUrl;
              setFormData({ ...formData, photos: newPhotos });
            }
          })
          .build();
        picker.setVisible(true);
      });
    });
  });
};
