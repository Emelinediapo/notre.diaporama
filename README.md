
    <div className="max-w-2xl mx-auto p-4">
      <Card>
        <CardContent className="p-4 space-y-4">
          <div>
            <Label>Votre nom</Label>
            <Input type="text" value={formData.name} onChange={(e) => setFormData({ ...formData, name: e.target.value })} />
          </div>

          <div>
            <Label>Votre lien avec les mariés</Label>
            <Select onValueChange={(value) => setFormData({ ...formData, relation: value })}>
              <SelectTrigger>
                <SelectValue placeholder="Sélectionnez votre lien" />
              </SelectTrigger>
              <SelectContent>
                <SelectItem value="famille_claire">Famille de Claire</SelectItem>
                <SelectItem value="famille_tristan">Famille de Tristan</SelectItem>
                <SelectItem value="amis">Amis</SelectItem>
                <SelectItem value="collegues_claire">Collègues de Claire</SelectItem>
                <SelectItem value="collegues_tristan">Collègues de Tristan</SelectItem>
                <SelectItem value="autre">Autre</SelectItem>
              </SelectContent>
            </Select>
          </div>

          {formData.photos.map((photo, index) => (
            <div key={index} className="border-t pt-4 space-y-2">
              <Label>Photo {index + 1}</Label>
              <Input type="date" value={photo.date} onChange={(e) => handleInputChange(e, index, "date")} />
              <Input type="text" placeholder="Lieu" value={photo.place} onChange={(e) => handleInputChange(e, index, "place")} />
              <Input type="text" placeholder="Légende" value={photo.caption} onChange={(e) => handleInputChange(e, index, "caption")} />
              <Button onClick={() => handleFileSelect(index)}>Sélectionner une photo</Button>
              {photo.preview && <img src={photo.preview} alt={`Preview ${index + 1}`} className="mt-2 w-32 h-32 object-cover" />}
            </div>
          ))}
        </CardContent>
      </Card>
    </div>
  );
}
